<template>
  <div class="name">popeyes</div>
  <div id="map" style="width: 100%; height: 100%"></div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const latitude = ref(0);
const longitude = ref(0);

onMounted(() => {
  if (!("geolocation" in navigator)) {
    return;
  }

  navigator.geolocation.getCurrentPosition(
    (pos) => {
      console.log(pos.coords.latitude, pos.coords.longitude);

      latitude.value = pos.coords.latitude;
      longitude.value = pos.coords.longitude;

      if (window.kakao && window.kakao.maps) {
        initMap();
      } else {
        const script = document.createElement("script");
        script.onload = () => kakao.maps.load(initMap);
        script.src =
          "//dapi.kakao.com/v2/maps/sdk.js?appkey=93c15b1cbc765ba774c3cf665538a8cc&libraries=services";
        document.head.appendChild(script);
      }
    },
    (err) => {
      alert(err.message);
    }
  );
});

const initMap = () => {
  const container = document.getElementById("map");
  let options = {
    center: new kakao.maps.LatLng(latitude.value, longitude.value),
    level: 3,
  };

  let map = new kakao.maps.Map(container, options);
  var imageSrc = "/image/marker-home.png",
    imageSize = new kakao.maps.Size(20, 20),
    imageOption = { offset: new kakao.maps.Point(27, 69) };

  var markerImage = new kakao.maps.MarkerImage(
    imageSrc,
    imageSize,
    imageOption
  );

  var positions = [
    {
      content: "<div>파파이스 강남점</div>",
      latlng: new kakao.maps.LatLng(37.49323319245009, 127.02932714667153),
    },
    {
      content: "<div>파파이스 구로디지털점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 화곡역점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 성남신흥점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 화정역점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 안양일번가점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 인하대역점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 공릉역점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 홍대점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 광화문점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 안산중앙점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
    {
      content: "<div>파파이스 성균관대점</div>",
      latlng: new kakao.maps.LatLng(37.48605610722263, 126.89717543026138),
    },
  ];

  function makeOverListener(map, marker, infowindow) {
    return function () {
      infowindow.open(map, marker);
    };
  }

  function makeOutListener(infowindow) {
    return function () {
      infowindow.close();
    };
  }

  for (var i = 0; i < positions.length; i++) {
    var marker = new kakao.maps.Marker({
      map: map,
      image: markerImage,
      position: positions[i].latlng,
    });

    var infowindow = new kakao.maps.InfoWindow({
      content: positions[i].content,
    });

    kakao.maps.event.addListener(
      marker,
      "mouseover",
      makeOverListener(map, marker, infowindow)
    );

    kakao.maps.event.addListener(
      marker,
      "mouseout",
      makeOutListener(infowindow)
    );
  }
};
</script>

<style lang="scss" scoped>
div .name {
  display: flex;
  font-size: 40px;
  font-weight: bold;
  justify-content: flex-start;
  align-items: center;
}
</style>
