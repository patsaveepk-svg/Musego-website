<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MuseGo</title>

<style>
body {
    font-family: sans-serif;
    margin: 0;
    background: #f5f5f5;
}

header {
    background: #8B5E3C;
    color: white;
    text-align: center;
    padding: 40px;
}

.container {
    padding: 20px;
}

.card {
    background: white;
    margin: 15px 0;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 3px 10px rgba(0,0,0,0.1);
}

.card img {
    width: 100%;
    height: 180px;
    object-fit: cover;
}

.card-content {
    padding: 15px;
}

button {
    margin-top: 8px;
    padding: 8px;
    border: none;
    background: #c89b6d;
    color: white;
    border-radius: 6px;
    width: 100%;
}

#trip-list li {
    background: white;
    margin: 5px 0;
    padding: 10px;
    border-radius: 6px;
    display: flex;
    justify-content: space-between;
}
</style>
</head>

<body>

<header>
<h1>MuseGo</h1>
<p>เที่ยวพิพิธภัณฑ์พระนครใน 1 วัน</p>
</header>

<div class="container">

<h2>เลือกสไตล์</h2>
<select id="style">
<option value="fun">สายสนุก</option>
<option value="history">สายความรู้</option>
<option value="chill">สายชิล</option>
</select>
<button onclick="generateTrip()">จัดทริปอัตโนมัติ</button>

<h2>พิพิธภัณฑ์</h2>

<!-- 1 -->
<div class="card">
<img src="https://images.unsplash.com/photo-1566073771259-6a8506099945">
<div class="card-content">
<h3>มิวเซียมสยาม</h3>
<button onclick="addToTrip('Museum Siam Bangkok')">เพิ่มลงทริป</button>
<button onclick="navigateTo('Museum Siam Bangkok')">นำทาง</button>
</div>
</div>

<!-- 2 -->
<div class="card">
<img src="https://images.unsplash.com/photo-1549893074-7a4e0f7c5d35">
<div class="card-content">
<h3>พิพิธภัณฑสถานแห่งชาติ พระนคร</h3>
<button onclick="addToTrip('National Museum Bangkok')">เพิ่มลงทริป</button>
<button onclick="navigateTo('National Museum Bangkok')">นำทาง</button>
</div>
</div>

<!-- 3 -->
<div class="card">
<img src="https://images.unsplash.com/photo-1529429617124-95b109e86bb8">
<div class="card-content">
<h3>นิทรรศน์รัตนโกสินทร์</h3>
<button onclick="addToTrip('Rattanakosin Exhibition Hall')">เพิ่มลงทริป</button>
<button onclick="navigateTo('Rattanakosin Exhibition Hall')">นำทาง</button>
</div>
</div>

<!-- 4 -->
<div class="card">
<img src="https://images.unsplash.com/photo-1504198453319-5ce911bafcde">
<div class="card-content">
<h3>พิพิธภัณฑ์ผ้า สมเด็จพระนางเจ้าสิริกิติ์</h3>
<button onclick="addToTrip('Queen Sirikit Museum of Textiles')">เพิ่มลงทริป</button>
<button onclick="navigateTo('Queen Sirikit Museum of Textiles')">นำทาง</button>
</div>
</div>

<!-- 5 -->
<div class="card">
<img src="https://images.unsplash.com/photo-1519681393784-d120267933ba">
<div class="card-content">
<h3>พิพิธภัณฑ์เหรียญกษาปณานุรักษ์</h3>
<button onclick="addToTrip('Coin Museum Bangkok')">เพิ่มลงทริป</button>
<button onclick="navigateTo('Coin Museum Bangkok')">นำทาง</button>
</div>
</div>

<!-- 6 -->
<div class="card">
<img src="https://images.unsplash.com/photo-1500530855697-b586d89ba3ee">
<div class="card-content">
<h3>พิพิธภัณฑ์บางลำพู</h3>
<button onclick="addToTrip('Banglamphu Museum')">เพิ่มลงทริป</button>
<button onclick="navigateTo('Banglamphu Museum')">นำทาง</button>
</div>
</div>

<h2>ทริปของฉัน</h2>
<ul id="trip-list"></ul>

<h2>แผนที่</h2>
<iframe id="mapFrame" width="100%" height="300"></iframe>

</div>

<script>
let trip = JSON.parse(localStorage.getItem("trip")) || [];

function addToTrip(place) {
    if (!trip.includes(place)) {
        trip.push(place);
        updateMap(place);
        save();
    } else {
        alert("มีแล้ว!");
    }
}

function removeItem(i) {
    trip.splice(i,1);
    save();
}

function save() {
    localStorage.setItem("trip", JSON.stringify(trip));
    render();
}

function render() {
    let list = document.getElementById("trip-list");
    list.innerHTML = "";
    trip.forEach((p,i)=>{
        list.innerHTML += `<li>${p} <button onclick="removeItem(${i})">ลบ</button></li>`;
    });
}

function generateTrip() {
    let s = document.getElementById("style").value;

    if(s=="fun") trip=["Museum Siam Bangkok","Banglamphu Museum"];
    if(s=="history") trip=["National Museum Bangkok","Rattanakosin Exhibition Hall"];
    if(s=="chill") trip=["Queen Sirikit Museum of Textiles","Coin Museum Bangkok"];

    updateMap(trip[0]);
    save();
}

function navigateTo(place){
    window.open("https://www.google.com/maps/search/?api=1&query="+place);
}

function updateMap(place){
    document.getElementById("mapFrame").src =
    "https://www.google.com/maps?q="+place+"&output=embed";
}

render();
</script>

</body>
</html>
