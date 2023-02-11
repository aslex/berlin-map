<script>
import {
  Viewer,
  Cartesian3,
  Math,
  Cesium3DTileset,
  GeoJsonDataSource,
  ClassificationType,
  IonResource,
  CesiumTerrainProvider,
  createOsmBuildings,
  Ion,
  Cesium3DTileStyle,
  Color,
} from "cesium";
import "../css/main.css";

Ion.defaultAccessToken = import.meta.env.VITE_CESIUM_TOKEN;

const viewer = new Viewer("cesiumContainer", {
  terrainProvider: new CesiumTerrainProvider({
    url: "https://www.virtualcitymap.de/datasource-data/globalterrain_5_9",
    requestVertexNormals: true,
  }),
});
viewer.camera.flyTo({
  destination: Cartesian3.fromDegrees(
    13.33963885585301,
    52.50395714015879,
    200
  ),
  orientation: {
    heading: Math.toRadians(0.0),
    pitch: Math.toRadians(-15.0),
  },
});

const berlinTilesetURL =
  "https://www.virtualcitymap.de/datasource-data/f892f6af-180a-4eef-917f-5ff03c260b32/tileset.json";

const tileset = viewer.scene.primitives.add(
  new Cesium3DTileset({
    url: berlinTilesetURL,
  })
);
tileset.style = new Cesium3DTileStyle({
  color: "color('blue')",
});
const buildingsTileset = viewer.scene.primitives.add(createOsmBuildings());
</script>
