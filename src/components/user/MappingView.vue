<template>
  <div>
    <div>영화관</div>
    <div>{{ moveLat }} / {{ moveLng }}</div>
    <div id="map" style="width: 500px; height: 400px"></div>
    <p><em>지도를 클릭해주세요!</em></p>
    <div id="clickLatlng"></div>
    <div class="btn" style="background-color: fuchsia" @click="addData()">
      add
    </div>
    <form></form>
    <div class="mb-1">
      <input
        type="text"
        class="form-control"
        id="nameInput"
        placeholder="name"
      />
    </div>
    <div class="mb-1" id="lat1">
      <input type="text" class="form-control" placeholder="latitude" />
    </div>
    <div class="mb-1" id="long1">
      <input type="text" class="form-control" placeholder="longitude" />
    </div>
  </div>
</template>
<script setup>
import { onMounted, ref } from "vue";

var latitude = ref(0);
var longitude = ref(0);
var latlng = ref(0);
var lat = ref(0);
var lng = ref(0);

let map = ref(0);
var m_markerImage = ref(0);
var m_imageSrc = ref(0);
var m_imageSize = ref(0);
var m_imageOption = ref(0);
var positions = [
  {
    content: "<div>에무시네마</div>",
    latlng: new kakao.maps.LatLng(37.5720343, 126.9689848),
  },

  {
    content: "<div>서울아트시네마</div>",
    latlng: new kakao.maps.LatLng(37.568038, 126.9695876),
  },

  {
    content: "<div>허리우드클래식</div>",
    latlng: new kakao.maps.LatLng(37.5728323, 126.9880012),
  },
  {
    content: "<div>아트하우스모모</div>",
    latlng: new kakao.maps.LatLng(37.5618588, 126.9468339),
  },
  {
    content: "<div>씨네큐브광화문</div>",
    latlng: new kakao.maps.LatLng(37.5697279, 126.9722881),
  },
  {
    content: "<div>아리랑시네센터</div>",
    latlng: new kakao.maps.LatLng(37.6002383, 127.0139101),
  },

  {
    content: "<div>KU시네마테크</div>",
    latlng: new kakao.maps.LatLng(37.5428904, 127.07307),
  },
  {
    content: "<div>인디스페이스</div>",
    latlng: new kakao.maps.LatLng(37.5571917, 126.9247586),
  },
  {
    content: "<div>아트나인</div>",
    latlng: new kakao.maps.LatLng(37.4847606, 126.9815207),
  },
  {
    content: "<div>필름포럼</div>",
    latlng: new kakao.maps.LatLng(37.5637568, 126.9441118),
  },

  {
    content: "<div>더숲 아트시네마</div>",
    latlng: new kakao.maps.LatLng(37.6541596, 127.0614397),
  },
  {
    content: "<div>낭만극장</div>",
    latlng: new kakao.maps.LatLng(37.573010846738704, 126.98790458732097),
  },

  {
    content: "<div>한국영상자료원</div>",
    latlng: new kakao.maps.LatLng(37.5804117, 126.8899473),
  },
];
function makeOverListener(map, m_marker, infowindow) {
  return function () {
    infowindow.open(map, m_marker);
  };
}
function makeOutListener(infowindow) {
  return function () {
    infowindow.close();
  };
}
function addMarkers() {
  // 기존 마커를 모두 제거합니다.
  if (window.markers) {
    window.markers.forEach((marker) => marker.setMap(null));
  }
  window.markers = [];

  // positions 배열을 돌면서 새로운 마커를 추가합니다.
  for (let i = 0; i < positions.length; i++) {
    var m_marker = new kakao.maps.Marker({
      map: map,
      image: m_markerImage,
      position: positions[i].latlng,
    });

    var infowindow = new kakao.maps.InfoWindow({
      content: positions[i].content,
    });

    kakao.maps.event.addListener(
      m_marker,
      "mouseover",
      makeOverListener(map, m_marker, infowindow)
    );
    kakao.maps.event.addListener(
      m_marker,
      "mouseout",
      makeOutListener(infowindow)
    );

    // 추가된 마커를 전역 변수에 저장
    window.markers.push(m_marker);
  }
}
function addData() {
  console.log("hello");
  let mData = {
    content: document.getElementById("nameInput").value,
    latlng: new kakao.maps.LatLng(lat, lng),
  };
  positions.push(mData);
  addMarkers();
}
const initMap = () => {
  var container = document.getElementById("map");
  let options = {
    center: new kakao.maps.LatLng(latitude.value, longitude.value),
    level: 3,
  };

  map = new kakao.maps.Map(container, options);

  (m_imageSrc = "/image/marker-movie.png"),
    (m_imageSize = new kakao.maps.Size(20, 20)),
    (m_imageOption = { offset: new kakao.maps.Point(27, 69) });

  m_markerImage = new kakao.maps.MarkerImage(
    m_imageSrc,
    m_imageSize,
    m_imageOption
  );

  var marker = new kakao.maps.Marker({
    position: map.getCenter(),
  });
  marker.setMap(map);
  kakao.maps.event.addListener(map, "click", function (mouseEvent) {
    latlng = mouseEvent.latLng;
    marker.setPosition(latlng);
    var message = "위도: " + latlng.getLat() + "/";
    lat = latlng.getLat();

    lng = latlng.getLng();
    message += "경도: " + latlng.getLng();
    var resultDiv = document.getElementById("clickLatlng");
    resultDiv.innerHTML = message;
    var latInput = document.querySelector("#lat1 input");
    var longInput = document.querySelector("#long1 input");

    latInput.value = lat;
    longInput.value = lng;
  });
  //
  //

  for (var i = 0; i < positions.length; i++) {
    var m_marker = new kakao.maps.Marker({
      map: map,
      image: m_markerImage,
      position: positions[i].latlng,
    });

    var infowindow = new kakao.maps.InfoWindow({
      content: positions[i].content,
    });

    kakao.maps.event.addListener(
      m_marker,
      "mouseover",
      makeOverListener(map, m_marker, infowindow)
    );
    kakao.maps.event.addListener(
      m_marker,
      "mouseout",
      makeOutListener(infowindow)
    );
  }
};
onMounted(() => {
  if (!("geolocation" in navigator)) {
    return;
  }

  navigator.geolocation.getCurrentPosition(
    (pos) => {
      console.log(pos.coords.latitude, pos.coords.longitude);

      latitude.value = pos.coords.latitude;
      longitude.value = pos.coords.longitude;

      //   initMap();

      if (window.kakao && window.kakao.maps) {
        initMap();
      } else {
        const script = document.createElement("script");
        /* global kakao */
        script.onload = () => kakao.maps.load(initMap);
        script.src =
          "//dapi.kakao.com/v2/maps/sdk.js?appkey=93c15b1cbc765ba774c3cf665538a8cc";
        document.head.appendChild(script);
      }
    },
    (err) => {
      alert(err.message);
    }
  );
});
</script>
<style lang="scss" scoped></style>
