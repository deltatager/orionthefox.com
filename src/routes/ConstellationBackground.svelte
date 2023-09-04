<script lang="ts">
  export let height: number
  export let width: number
  export let animDelaySec: number

  const SVG_NS = 'http://www.w3.org/2000/svg'

  interface PathSegment {
    command: string
    x: number
    y: number
  }

  function createPathStr(scale: number, pathSegments: PathSegment[]) {
    return pathSegments.reduce((a, e) => `${a} ${e.command} ${e.x * scale} ${e.y * scale} `, '')
  }

  const orionPath = [
    { command: 'M', x: 0, y: 3 },
    { command: 'L', x: 1, y: 20 },
    { command: 'L', x: 5, y: 18 },

    { command: 'M', x: 28, y: 77 },
    { command: 'L', x: 31.5, y: 73 },
    { command: 'L', x: 35, y: 69 },

    { command: 'M', x: 15, y: 44 },
    { command: 'L', x: 33, y: 35 },
    { command: 'L', x: 41, y: 48 },
    { command: 'L', x: 35, y: 69 },
    { command: 'L', x: 51, y: 99 },
    { command: 'L', x: 22, y: 104 },
    { command: 'L', x: 28, y: 77 },
    { command: 'L', x: 15, y: 44 },
    { command: 'L', x: 9, y: 36 },
    { command: 'L', x: 5, y: 18 },
    { command: 'L', x: 9, y: 0 },

    { command: 'M', x: 41, y: 48 },
    { command: 'L', x: 72, y: 45 },

    { command: 'M', x: 67, y: 34 },
    { command: 'L', x: 71, y: 39 },
    { command: 'L', x: 72, y: 45 },
    { command: 'L', x: 71, y: 50 },
    { command: 'L', x: 68, y: 61 },
    { command: 'L', x: 65, y: 64 }
  ]

  function getPairs<T>(arr: T[]): T[][] {
    return arr.map((v, i) => arr.slice(i + 1).map((w) => [v, w])).flat()
  }

  function isWithinThreshold(
    originX: number,
    originY: number,
    targetX: number,
    targetY: number,
    threshold: number
  ) {
    return (
      originY - targetY <= threshold &&
      originY - targetY >= -threshold &&
      originX - targetX <= threshold &&
      originX - targetX >= -threshold
    )
  }

  function setProps(el: Element, classArr: string[], attrArr: { name: string; val: string }[]) {
    if (el !== undefined) {
      if (classArr !== undefined && classArr.length && Array.isArray(classArr)) {
        classArr.forEach(function (clas) {
          el.classList.add(clas)
        })
      }
      if (attrArr !== undefined && attrArr.length && Array.isArray(attrArr)) {
        attrArr.forEach(function (attr) {
          el.setAttribute(attr.name, attr.val)
        })
      }
    }
  }

  function setCoords(
    svgEl: SVGElement,
    c: Element,
    rX: string,
    rY: string,
    fill: string,
    isRandom: string
  ) {
    c.setAttribute('cx', rX)
    c.setAttribute('cy', rY)
    c.setAttribute('fill', fill)
    c.setAttribute('r', Number.isInteger(isRandom) ? isRandom : '2')
    svgEl.appendChild(c)
  }

  function drawPath(svgEl: SVGElement, pathStr: string, x: number, y: number) {
    let pathEl = document.createElementNS(SVG_NS, 'path') as SVGGeometryElement
    setProps(
      pathEl,
      [],
      [
        {
          name: 'id',
          val: 'constellation'
        },
        {
          name: 'fill',
          val: 'none'
        },
        {
          name: 'stroke',
          val: '#fff'
        },
        {
          name: 'style',
          val: 'opacity: .5;'
        },
        {
          name: 'stroke-width',
          val: '2'
        },
        {
          name: 'd',
          val: pathStr
        },
        {
          name: 'transform',
          val: `translate(${x}, ${y})`
        }
      ]
    )

    let total_length = pathEl.getTotalLength()
    pathEl.setAttribute('stroke-dasharray', total_length.toString())
    pathEl.setAttribute('stroke-dashoffset', total_length.toString())
    svgEl?.appendChild(pathEl)
  }

  function drawConstellation(svgEl: SVGElement, positionX: number, positionY: number) {
    const stringPath = createPathStr(width > 400 ? 2 : 0.75, orionPath)

    drawPath(svgEl, stringPath, positionX, positionY)

    let pathSegments: any[] = stringPath.match(/\w\s\d+\s\d+/gi) ?? []

    pathSegments
      .map((e) => e.replace(/[MLZ]\s/gi, ''))
      .forEach((p) => {
        const circle = document.createElementNS(SVG_NS, 'circle')
        const x = +p.match(/\d+/)
        const y = +p.match(/\d+$/)

        setProps(
          circle,
          ['cStar'],
          [
            {
              name: 'stroke-width',
              val: '10'
            },
            {
              name: 'stroke',
              val: 'rgba(225,225,225,.1)'
            },
            {
              name: 'r',
              val: (Math.random() * (4 - 1.5) + 1.5).toFixed(2)
            },
            {
              name: 'transform',
              val: `translate(${x + positionX}, ${y + positionY})`
            }
          ]
        )

        svgEl.appendChild(circle)
      })
  }

  function drawAnimatedStars(
    svgEl: SVGElement,
    height: number,
    width: number,
    animDelaySec: number
  ) {
    const nbAnimatedStars = width >= 1000 && height >= 600 ? 400 : 200

    for (let i = 0; i < nbAnimatedStars; i++) {
      const circle = document.createElementNS(SVG_NS, 'circle') as SVGGeometryElement

      setProps(
        circle,
        ['animate'],
        [
          {
            name: 'style',
            val: `animation-delay: ${(Math.random() * (animDelaySec * -1)).toFixed(2)}s`
          }
        ]
      )
      setCoords(
        svgEl,
        circle,
        (Math.random() * width).toFixed(2),
        (Math.random() * height).toFixed(2),
        '#fff',
        '2'
      )
    }
  }

  function drawStars(svgEl: SVGElement, height: number, width: number) {
    const staticStars: Element[] = []

    // Stars Loop
    for (let i = 0; i < 300; i++) {
      const circle = document.createElementNS(SVG_NS, 'circle')

      setCoords(
        svgEl,
        circle,
        (Math.random() * width).toFixed(2),
        (Math.random() * height).toFixed(2),
        '#fff',
        (Math.random() * 2.5).toFixed(2)
      )

      staticStars.push(circle)
    }

    const thresholdDistance = width >= 1000 && height >= 600 ? 40 : 20
    const pairs = getPairs(staticStars)
    // Trace lines between static stars closer than threshold
    pairs.forEach(([origin, target]) => {
      const originX = +(origin.getAttribute('cx') ?? 0)
      const originY = +(origin.getAttribute('cy') ?? 0)
      const targetX = +(target.getAttribute('cx') ?? 9999)
      const targetY = +(target.getAttribute('cy') ?? 9999)

      if (isWithinThreshold(originX, originY, targetX, targetY, thresholdDistance)) {
        const path = document.createElementNS(SVG_NS, 'path')
        setProps(
          path,
          [],
          [
            {
              name: 'fill',
              val: 'none'
            },
            {
              name: 'stroke',
              val: '#fff'
            },
            {
              name: 'style',
              val: 'opacity: .25'
            },
            {
              name: 'stroke-width',
              val: '1'
            },
            {
              name: 'd',
              val: `M ${originX} ${originY} L ${targetX} ${targetY}`
            }
          ]
        )
        svgEl.appendChild(path)
      }
    })
  }

  function draw(
    svgEl: SVGElement | undefined,
    height: number,
    width: number,
    animDelaySec: number
  ) {
    if (typeof document === 'undefined' || !svgEl) return

    svgEl.replaceChildren()

    drawStars(svgEl, height, width)
    drawAnimatedStars(svgEl, height, width, animDelaySec)
    drawConstellation(svgEl, width > 400 ? width * 0.66 : width * 0.80, width > 400 ? 200 : 320)
  }

  let svg: SVGElement
  $: draw(svg, height, width, animDelaySec)
</script>

<svg bind:this={svg} {width} {height} style="--anim-delay: {animDelaySec}s" />

<style>
  svg {
    padding: 0;
    margin: 0;
    border: 0;
    position: absolute;
    z-index: -9999;
    background-color: #fff0;
  }
</style>
