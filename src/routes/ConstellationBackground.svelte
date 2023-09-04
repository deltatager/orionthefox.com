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

  function pauseAnimationFor3s(svg: SVGElement | undefined) {
    let c = svg?.querySelectorAll('.animate')

    for (let i = 0, circle = (c?.length ?? 1) / 1.4; i < circle; i++) {
      c?.[i].classList.add('paused')
    }

    setTimeout(function () {
      for (var i = 0, circle = c?.length ?? 1; i < circle; i++) {
        c?.[i].classList.remove('paused')
      }
    }, 3000)
  }

  function setProps(el: Element, classArr: string[], attrArr: any[]) {
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

  function setCoords(c: Element, rX: string, rY: string, fill: string, isRandom: string) {
    c.setAttribute('cx', rX)
    c.setAttribute('cy', rY)
    c.setAttribute('fill', fill)
    c.setAttribute('r', Number.isInteger(isRandom) ? isRandom : '2')
    svg?.appendChild(c)
  }

  function drawPath(svgEl: SVGElement, pathStr: string) {
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
          val: 2
        },
        {
          name: 'd',
          val: pathStr
        }
      ]
    )

    let total_length = pathEl.getTotalLength()
    pathEl.setAttribute('stroke-dasharray', total_length.toString())
    pathEl.setAttribute('stroke-dashoffset', total_length.toString())
    svgEl?.appendChild(pathEl)
  }

  const path = createPathStr(2, [
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
  ])

  function drawConstellation(svgEl: SVGElement) {
    drawPath(svgEl, path)
    // pauseAnimationFor3s(svgEl)

    let pathSegments: any[] = path.match(/\w\s\d+\s\d+/gi) ?? []
    let pathApexes = pathSegments.map((e) => e.replace(/[MLZ]\s/gi, ''))

    // Create (n) amount of a constellation's star
    for (var i = 0; i < pathApexes.length; i++) {
      let circle = document.createElementNS(SVG_NS, 'circle')

      let x = pathApexes[i].match(/\d+/)
      let y = pathApexes[i].match(/\d+$/)

      setProps(
        circle,
        ['cStar'],
        [
          {
            name: 'stroke-width',
            val: 10
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
            val: `translate(${x}, ${y})`
          }
        ]
      )

      svgEl?.appendChild(circle)
    }
  }

  function main(svgEl: SVGElement | undefined, ViewportX: number, ViewportY: number) {
    if (typeof document === 'undefined' || !svgEl) return

    svgEl.replaceChildren()

    let randomX = 0
    let randomY = 0
    let randomR = 0
    let randomDelay = 0

    function drawStars() {
      let allCoords: Element[] = []
      let n = ViewportX >= 1000 && ViewportY >= 600 ? 40 : 20
      let n1 = ViewportX >= 1000 && ViewportY >= 600 ? 400 : 200

      // Stars Loop
      for (var i = 0, stars = 300; i < stars; i++) {
        let circle = document.createElementNS(SVG_NS, 'circle')
        randomX = +(Math.random() * (ViewportX - 0) + 0).toFixed(2)
        randomY = +(Math.random() * (ViewportY - 0) + 0).toFixed(2)
        randomR = +(Math.random() * 2.5).toFixed(2)
        setCoords(circle, randomX.toString(), randomY.toString(), '#fff', randomR.toString())
        allCoords.push(circle)
      }

      // Animated Stars Loop
      for (let i = 0, animStars = n1; i < animStars; i++) {
        let circle = document.createElementNS(SVG_NS, 'circle') as SVGGeometryElement

        randomX = +(Math.random() * (ViewportX - 0) + 0).toFixed(2)
        randomY = +(Math.random() * (ViewportY - 0) + 0).toFixed(2)
        randomDelay = +(Math.random() * (animDelaySec * -1)).toFixed(2)

        circle.classList.add('animate')
        circle.style.animationDelay = randomDelay + 's'
        setCoords(circle, randomX.toString(), randomY.toString(), '#fff', '2')

        // Causing additional 2-3s of JS execution
        // allCoords.push(circle);
      }

      // For each circle get its coords
      allCoords.forEach(function (el) {
        let elX = +el.attributes['cx'].value,
          arrElX = 0
        let elY = +el.attributes['cy'].value,
          arrElY = 0
        let pathStr = ''
        let i = 0
        let path
        let arr

        for (i, arr = allCoords; i < arr.length; i++) {
          arrElX = arr[i].attributes['cx'].value
          arrElY = arr[i].attributes['cy'].value
          // Check for each circle whether other circles' coordinates enter to the its 40x40 range
          // If so, create a path with M (circle's coordinates) as well as L (other's coordinates)
          // and then put the path to "d" attribute
          if (elY - arrElY <= n && elY - arrElY >= -n && elX - arrElX <= n && elX - arrElX >= -n) {
            path = document.createElementNS(SVG_NS, 'path')
            pathStr = 'M' + ' ' + elX + ' ' + elY + ' L' + ' ' + arrElX + ' ' + arrElY
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
                  val: 'opacity: .05;'
                },
                {
                  name: 'stroke-width',
                  val: 1
                },
                {
                  name: 'd',
                  val: pathStr
                }
              ]
            )
            svgEl?.appendChild(path)
          }
        }
      })
      return
    }

    drawStars()
    // drawConstellation(svgEl)
  }

  let svg: SVGElement
  $: main(svg, width, height)
</script>

<svg bind:this={svg} {width} {height} style="--anim-delay: {animDelaySec}s"/>

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
