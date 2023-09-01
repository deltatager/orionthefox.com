<script lang="ts">
  import QRCodeStyling, { type DotType, type Gradient, type Options } from 'qr-code-styling-new'

  export let data: string
  export let image: string
  export let label: string
  export let dotsOptions: {
        type?: DotType
        color?: string
        gradient?: Gradient
    }

  let canvasElement: HTMLElement | undefined

  const qrOptions: Partial<Options> = {
    width: 300,
    height: 300,
    type: 'canvas',
    data,
    image,
    dotsOptions,
    imageOptions: {
      crossOrigin: 'anonymous',
      margin: 10,
    },
	cornersSquareOptions: {
		type: 'extra-rounded'
	},
	cornersDotOptions: {
		type: 'dot'
	}
  }

  $: if (typeof window !== 'undefined') {
    const qrCode = new QRCodeStyling(qrOptions)
    qrCode.append(canvasElement)
  }
</script>

<div style='margin: 8px; text-align: center'>
	<div bind:this={canvasElement} />
	<span>{label}</span>
</div>
