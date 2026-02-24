# AR.js Image + Buttons + Popups (WebAR)

This project provides a simple WebAR experience using A-Frame + AR.js:
- An image appears anchored to a marker.
- Multiple on-image buttons you can tap.
- Each button toggles a text bubble popup with info.

Out of the box, it uses the default "hiro" pattern marker and a sample image texture. You can customize the image and the info points.

## Files
- `index.html` — The AR scene (A-Frame + AR.js) with dynamic POIs.
- `server.js` — Minimal HTTPS static server for local testing.
- `.gitignore`

## Run locally with HTTPS (required for mobile camera access)

1) Install Node.js (v16+ recommended).

2) Install dependencies (none needed) and start the server:

```bash
node server.js
```

On first run, the server will generate a self-signed certificate via `openssl`. Ensure `openssl` is installed on your machine.

3) Open the app:
- On desktop: https://localhost:8443
- On your phone: use the LAN URL shown in the console, e.g. `https://192.168.x.x:8443`

4) Accept the self-signed certificate warning in your browser, then allow camera permissions.

5) Point your camera at the "hiro" marker to see the AR content:
- Print or display the marker image: https://raw.githubusercontent.com/AR-js-org/AR.js/master/three.js/data/markers/patt.hiro.png

6) Tap one of the blue buttons to toggle its info popup. Tap the background image to close all popups.

## Customize

- Change the base image texture:
  - In `index.html`, update the `<img id="mainImage" ...>` src to your file (e.g., `./assets/my-image.png`).
  - Add your file under an `assets/` folder.

- Edit the data points (labels, descriptions, positions):
  - In `index.html`, modify the `POI_DATA` array. Offsets are in meters relative to the center of the image, which is laid flat on the marker (X right, Y up, Z toward camera). The scene rotates the content `-90` on X so it lies on the marker.

- Use a custom marker:
  - Convert your marker image to a `.patt` file using AR.js Marker Training: https://jeromeetienne.github.io/AR.js/three.js/examples/marker-training/examples/generator.html
  - Save the `.patt` into a `markers/` folder and in `index.html` change the marker element from:
    ```html
    <a-marker type="pattern" preset="hiro">
    ```
    to
    ```html
    <a-marker type="pattern" url="./markers/your-marker.patt">
    ```

## Deploy on the web (optional)

Any static host with HTTPS works (GitHub Pages, Netlify, Vercel, etc.). Steps are similar:
- Push this repo to GitHub.
- Deploy the static `index.html`.
- Ensure the page is served over HTTPS so camera access works on mobile.

## Notes
- Some Android/Chrome versions allow camera on HTTP if using localhost, but on mobile over LAN you need HTTPS.
- Performance depends on device. Ensure good lighting and a high-contrast marker for best tracking.
- The included raycaster is set to interact with `.clickable` entities and the `.bg-intercept` image plane.
