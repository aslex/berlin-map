<script lang="ts">
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
  ScreenSpaceEventHandler,
  ScreenSpaceEventType,
  Cesium3DTileStyle,
  Color,
  Timeline,
  Entity,
} from "cesium";

Ion.defaultAccessToken = import.meta.env.VITE_CESIUM_TOKEN;

const viewer = new Viewer("cesiumContainer", {
  infoBox: false,
  terrainProvider: new CesiumTerrainProvider({
    url: "https://www.virtualcitymap.de/datasource-data/globalterrain_5_9",
  }),
});

viewer.camera.flyTo({
  destination: Cartesian3.fromDegrees(
    13.33974614421162,
    52.50259219984586,
    100
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

let selected = new Entity();
const handler = new ScreenSpaceEventHandler(viewer.scene.canvas);
tileset.tileLoad;
handler.setInputAction(function (movement) {
  const item = viewer.scene.pick(movement.position);
  if (!item) return;
  console.log("move!", item.content.tileset.root.children);
  console.log("move!", item._content);
  // item.content.model.outlineColor
  item.content.tile.style = new Cesium3DTileStyle({
    color: 'color("red")',
  });
  selected = item;
}, ScreenSpaceEventType.LEFT_CLICK);

export default {
  data() {
    return {
      tileset,
      viewer,
      selectedObject: selected,
    };
  },
  methods: {
    selectObject: function (tile) {
      this.selectObject = tile;
    },
  },
};
</script>
