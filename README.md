[![Netlify Status](https://api.netlify.com/api/v1/badges/4cf817ac-08c3-4907-b38d-d73c341ba744/deploy-status)](https://rangiwahia.netlify.app/)
# Application of threejs-dem-visualizer

All credits go to [@orabazu](https://github.com/orabazu). I have simply changed the DEM files and published to Netlify.

Here is the full explanation of the workflow by [@orabazu](https://github.com/orabazu):

- https://github.com/orabazu/threejs-dem-visualizer
- https://medium.com/@zubazor/visualizing-a-mountain-using-three-js-landsat-and-srtm-26275c920e34

Below are my minor comments

### Prerequisites

- Digital Elevation Model (DEM) in `.tif` format. While the CRS doesn't matter, it's beneficial to have a metric one.
- Overlay Image in `.jpg` format. Initially, I used an aerial image with a resolution of 0.3m / pix, but it was too high for the browser to render, so I rescaled it to a coarser one.
- The extent of the DEM and Image should be the same!
- Both the DEM and Image files should be placed in the `src/textures` folder. If they are placed elsewhere, the paths will need to be updated in `index.js`.
- You should have `node.js`, `npm` and `yarn` installed. I used Node Version Manager on Pop OS 22.04 following [this instruction](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-22-04#option-3-installing-node-using-the-node-version-manager). `npm` and `yarn` are straightforward to install through `apt` or `aptitude`:

```
node -v # 20.9.0
sudo apt install npm
# or
# sudo aptitude install npm
npm install --global yarn
```

### Overlay Image

The quickest way to get a `.jpg` image from a `.tif` is to run `gdal_translate`

```bash
gdal_translate -of JPEG -scale -co worldfile=no aerial_cropped.tif output.jpg
```

### Installation

```
git clone https://github.com/atsyplenkov/threejs-dem-visualizer-test.git
cd threejs-dem-visualizer-test

yarn install
```

### Usage

1. Replace `rangi_dem.tif` with your DEM and `rangi_aerial.jpg` with your Image.
2. Change file names in `index.js` accordingly (lines 20-21).
3. Change the z-factor (line 142 in `index.js`).
4. Generate all js/css bundles.

```
yarn build
```

1. Development

```
yarn start
```

1. Go to `localhost:8080` to see your project live!

### Deployment

As a novice web developer, I simply followed the instructions from [YouTube](https://www.youtube.com/watch?v=2x9AuM6xpxg).
In a nutshell:

1. Go to Netlify.
2. Login using GitHub.
3. Create a project using your git repository.
4. Specify build commands (this is the most crucial moment in the whole deployment process).
Build command: `npm run build`
Publish directory: `build`
5. Visit your website.
