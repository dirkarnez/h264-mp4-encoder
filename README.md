[h264-mp4-encoder-playground](https://dirkarnez.github.io/h264-mp4-encoder-playground)
======================================================================================
### Using
- [TrevorSundberg/h264-mp4-encoder: H264 encoder + MP4 output for the web](https://github.com/TrevorSundberg/h264-mp4-encoder)

### Snippets
- Headless mp4 generation (no canvas)
```js
  HME.createH264MP4Encoder().then(async encoder => {
    encoder.initialize();

    const frames = 100;
    for (let i = 0; i <= frames; ++i) {


      // Must be a multiple of 2.
      encoder.width = 100;
      encoder.height = 100;

      encoder.initialize();

      // Add a single gray frame, the alpha is ignored.
      encoder.addFrameRgba(new Uint8Array(encoder.width * encoder.height * 4).fill(128))

      // For canvas:
      // encoder.addFrameRgba(ctx.getImageData(0, 0, encoder.width * encoder.height).data);

      // or just ImageData
      var imageData = new ImageData(100, 100);
      // do stuff
      encoder.addFrameRgba(imageData);
  
      encoder.finalize();
    }

    encoder.finalize();
    const uint8Array = encoder.FS.readFile(encoder.outputFilename);
    download(URL.createObjectURL(new Blob([uint8Array], { type: "video/mp4" })))
    encoder.delete();
  })
```
