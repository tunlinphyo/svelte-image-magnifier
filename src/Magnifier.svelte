<div class="container">
  <div class="thumb" bind:this={thumbEl}>
    <div class={`zoom ${show ? 'show' : ''}`}
      style={`
        clip-path: polygon(
          0% 0%,
          0% 100%,
          ${percentageX}% 100%,
          ${percentageX}% ${percentageY}%,
          calc(${percentageX}% + 200px) ${percentageY}%,
          calc(${percentageX}% + 200px) calc(${percentageY}% + 200px),
          ${percentageX}% calc(${percentageY}% + 200px),
          ${percentageX}% 100%,
          100% 100%,
          100% 0%
        );
      `}
    ></div>
    <div class="view-img"
      style={`background-image: url(${image})`}
    ></div>
  </div>
  <div class={`preview ${show ? 'show' : ''}`}
    style={`
      width: ${thumbBCR ? thumbBCR.width + 'px' : 0};
      height: ${thumbBCR ? thumbBCR.height + 'px' : 0};
    `}
  >
    <div class="large"
      style={`
        transform: translate(${-percentageX.toFixed(0)}%, ${-percentageY.toFixed(0)}%);
      `}
    >
      <img src={largeImage} alt="large">
    </div>
  </div>
</div>

<style>
  .container {
    width: 100%;
    height: 0;
    padding-top: 100%;
    position: relative;
    background-color: #f4f4f4;
  }
  .thumb {
    position: absolute;
    z-index: 0;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    cursor: crosshair;
  }
  .zoom {
    position: absolute;
    top: 0; left: 0;
    width: 100%;
    height: 100%;
    background-color: #0005;
    opacity: 0;
    pointer-events: none;
    transition: opacity .25s ease;
  }
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .view-img {
    width: 100%;
    height: 100%;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
  }
  .preview {
    position: absolute;
    z-index: 1;
    top: 0;
    left: 100%;
    overflow: hidden;
    opacity: 0;
    pointer-events: none;
    box-shadow: 3px 3px 10px rgba(0,0,0,0.15);
    transition: opacity .25s ease;
  }
  .show {
    opacity: 1;
  }
  .large {
    position: absolute;
    top: 0;
    left: 0;
    width: 300%;
    height: 300%;
  }
</style>

<script>
  import {onMount} from 'svelte'

  export let image
  export let largeImage

  let thumbEl
  let percentageX = 0, percentageY = 0
  let show = false
  let thumbBCR

  onMount(() => {
    addEventListeners()
    return () => removeEventListeners()
  })

  function onMouseEnter(event) {
    show = true
    window.requestAnimationFrame(() => handleMouseMove(event))
  }
  function onMouseMove(event) {
    if (!show) show = true
    window.requestAnimationFrame(() => handleMouseMove(event))
  }
  function handleMouseMove(event) {
    thumbBCR = thumbEl.getBoundingClientRect()
    let startX = event.pageX || (event.touches ? event.touches[0].pageX : 0)
    let startY = event.pageY || (event.touches ? event.touches[0].pageY : 0)
    startX -= 100
    startY -= 100
    const currentY = Math.max(startY - thumbBCR.top - window.scrollY, 0)
    const maxY = thumbBCR.height - 200
    const y = Math.min(currentY, maxY)

    const currentX = Math.max(startX - thumbBCR.left, 0)
    const maxX = thumbBCR.width - 200
    const x = Math.min(currentX, maxX)

    percentageX = x / thumbBCR.width * 100
    percentageY = y / thumbBCR.height * 100
  }
  function onMouseLeave(event) {
    show = false
  }
  function addEventListeners() {
    if (!thumbEl) return
    thumbEl.addEventListener('mouseenter', onMouseEnter)
    thumbEl.addEventListener('mousemove', onMouseMove)
    thumbEl.addEventListener('mouseleave', onMouseLeave)
  }
  function removeEventListeners() {
    thumbEl.removeEventListener('mouseenter', onMouseEnter)
    thumbEl.removeEventListener('mousemove', onMouseMove)
    thumbEl.removeEventListener('mouseleave', onMouseLeave)
  }
</script>
