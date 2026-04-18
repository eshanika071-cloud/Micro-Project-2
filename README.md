<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Music Playlist Manager</title>

<style>
  * {
  box-sizing: border-box;
}
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #000;
  color: white;
}
#searchInput {
  outline: none;
  transition: 0.2s ease;
}

#searchInput:focus {
  box-shadow: 0 0 10px #8a2be2;
}

.left {
  display: flex;
  align-items: center;
  gap: 10px;
  padding-left: 20px;
}

#cover {
  width: 50px;
  height: 50px;
  border-radius: 6px;
}

/* Layout */
.app {
  display: flex;
  height: 100vh;
}

/* Sidebar */
.sidebar {
  width: 80px;
  background: #000;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px;
}

.sidebar div {
  margin: 15px 0;
  cursor: pointer;
}

/* Main */
.main {
  margin-left: 70px;
  padding: 20px;
}
.main {
  flex: 1;
  background: #121212;
  padding: 20px;
  overflow-y: auto;
}

/* Topbar */
.topbar {
  display: flex;
  justify-content: space-between;
}

.search {
  background: #222;
  padding: 10px;
  border-radius: 20px;
  border: none;
  color: white;
  width: 250px;
}

/* Inputs */
.input-box {
  margin-top: 20px;
}

input {
  padding: 10px;
  margin: 5px;
  border-radius: 6px;
  border: none;
  background: #111;
  color: white;
}

button {
  padding: 10px;
  margin: 5px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

/* Buttons */
.add-btn { background: #4cc9f0; }
.shuffle-btn { background: purple; color: white; }
.song-info {
  cursor: pointer;
}

.song-info b:not(.liked-song) {
  color: #4cc9f0;
}

.play-icon {
  opacity: 0;
  margin-left: 10px;
  cursor: pointer;
  transition: 0.3s;
}

li:hover .play-icon {
  opacity: 1;
  color: #4cc9f0;
}

.active {
  background: #2a2a2a;
}

/* Playlist */
ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  background: #181818;
  margin: 10px 0;
  padding: 10px;
  border-radius: 8px;
}

.delete-btn {
  background: red;
  color: white;
}

/* Cards */
.cards {
  display: flex;
  gap: 10px;
  margin-top: 20px;
}

.card {
  background: #181818;
  padding: 10px;
  border-radius: 10px;
  cursor: pointer;
  width: 150px;
}

.card:hover {
  background: #282828;
}

/* Player */
.player {
  position: fixed;
  bottom: 0;
  left: 70px;
  width: calc(100% - 70px);
  background: #121212;
  border-top: 1px solid #333;
  padding: 10px 20px;

  display: flex;
  justify-content: space-between;
  align-items: center;

  transition: 0.3s ease;
  z-index: 1000;
}

.player.shifted {
  width: calc(100% - 70px - 320px);
}

.left {
  width: 25%;
  padding-left: 20px;
}

.center {
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  
}

.right {
  width: 25%;
  
}

.time {
  font-size: 12px;
  color: #aaa;
  margin-top: 5px;
}

.controls button {
  font-size: 24px;
  margin: 0 10px;
  padding: 10px;
  border-radius: 10px;
  transition: 0.2s;
}

.controls button:hover {
  background: #282828;
  transform: scale(1.1);
}

#playBtn {
  font-size: 28px;
  border: 2px solid white;
  padding: 12px 18px;
  border-radius: 12px;
}

#progress {
  width: 70%;
  margin-top: 8px;
}

#nowPlaying {
  font-weight: bold;
  color: #4cc9f0;
}

.controls button {
  background: none;
  color: white;
  font-size: 18px;
}


/* LEFT */
.left {
  display: flex;
  align-items: center;
  gap: 10px;
  width: 25%;
}

#cover {
  width: 55px;
  height: 55px;
  border-radius: 6px;
}

/* CENTER */
.center {
  width: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* CONTROLS */
.top-controls {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 5px;
}

.top-controls button {
  background: none;
  border: none;
  color: white;
  font-size: 18px;
  cursor: pointer;
}

#playBtn {
  font-size: 22px;
  border: 2px solid white;
  border-radius: 50%;
  padding: 10px 14px;
}

/* PROGRESS */
.progress-container {
  display: flex;
  align-items: center;
  gap: 10px;
  width: 100%;
}

#progress {
  width: 100%;
}

/* RIGHT */
.right {
  width: 25%;
  display: flex;
  align-items: center;
  gap: 10px;
  justify-content: flex-end;
}
.queue-panel {
  position: fixed;
  top: 0;
  right: 0;
  width: 320px;
  height: 100vh;
  background: #0f0f0f;
  color: white;
  padding: 20px;
  overflow-y: auto;
  z-index: 99999;
  box-shadow: -10px 0 40px rgba(0,0,0,0.6);

  transform: translateX(100%);
  transition: transform 0.3s ease;
}

.queue-panel.active {
  transform: translateX(0);
}

.queue-panel h3 {
  margin-bottom: 10px;
}

.queue-panel ul {
  list-style: none;
  padding: 0;
}

.queue-panel li {
  padding: 8px;
  border-radius: 5px;
}

.queue-panel li.active {
  background: #2a2a2a;
  color: #4cc9f0;
}
.sidebar {
  position: fixed;
  left: 0;
  top: 0;
  width: 70px;
  height: 100vh;
  overflow-y: auto;
  background: #000;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 20px;
  gap: 20px;
}

.nav-btn {
  background: none;
  border: none;
  color: white;
  font-size: 22px;
  cursor: pointer;
  transition: 0.2s;
}

.nav-btn:hover {
  color: #4cc9f0;
  transform: scale(1.2);
}

.nav-btn.active {
  color: #4cc9f0;
}
.index {
  width: 30px;
  display: inline-block;
}

.num {
  display: inline;
}

.play-hover {
  display: none;
  cursor: pointer;
  color: #4cc9f0;
}

/* swap on hover */
li:hover .num {
  display: none;
}

li:hover .play-hover {
  display: inline;
}
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.left-part {
  display: flex;
  align-items: center;
  gap: 15px;
}

/* index (number/play) */
.index {
  width: 20px;
  text-align: center;
}

.num {
  display: inline;
}

.play-hover {
  display: none;
  cursor: pointer;
  color: #4cc9f0;
}

/* swap */
li:hover .num {
  display: none;
}

li:hover .play-hover {
  display: inline;
}
.play-hover {
  transition: 0.2s;
}
button.active {
  color: #4cc9f0;
  transform: scale(1.2);
}


/* Header */
.queue-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 25px;
}

.queue-header button {
  background: none;
  border: none;
  color: white;
  font-size: 20px;
  cursor: pointer;
}

.sidebar {
  z-index: 1000;
}
.player {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  transition: 0.3s ease;
}

.player.shifted {
  width: calc(100% - 320px); /* same as queue width */
}
.player.shifted {
  margin-right: 320px;
}
/* HEADER */
.queue-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 25px;
}

/* NOW PLAYING */
.now-card {
  display: flex;
  gap: 12px;
  align-items: center;
  margin-bottom: 25px;
}

.now-card img {
  width: 65px;
  height: 65px;
  border-radius: 8px;
  object-fit: cover;
}

.text {
  display: flex;
  flex-direction: column;
}

#qTitle {
  font-size: 15px;
  font-weight: bold;
  color: #1db954;
}

#qArtist {
  font-size: 12px;
  color: #b3b3b3;
}

/* NEXT LIST */
.next-list ul {
  padding: 0;
}

.next-list li {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 10px;
  border-radius: 8px;
  cursor: pointer;
  transition: 0.2s;
}

.next-list li:hover {
  background: rgba(255,255,255,0.08);
}

.next-list img {
  width: 45px;
  height: 45px;
  border-radius: 6px;
  object-fit: cover;
}
.liked-song {
  color: #ff4da6;
  font-weight: bold;
}
.actions button {
  font-size: 14px;
  padding: 6px 10px;
  border-radius: 8px;
  background: #222;
  color: white;
}

.actions button:hover {
  background: #444;
}
.modal {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.7);
  justify-content: center;
  align-items: center;
}

.modal-content {
  background: #111;
  padding: 20px;
  border-radius: 10px;
  width: 300px;
}

.modal-content button {
  width: 100%;
  margin-top: 10px;
}
.playlist-item {
  display: flex;
  justify-content: space-between;
  align-items: center;   /* ✅ THIS FIXES ALIGNMENT */
  width: 100%;
  padding: 5px 8px;
  font-size: 14px;
}
.playlist-item button {
  background: none;
  border: none;
  color: red;
  cursor: pointer;
  font-size: 14px;   /* smaller */
  padding: 2px;
}
.actions button {
  background: none;
  border: none;
  color: red;
  font-size: 16px;
  cursor: pointer;
}
.playlist-item span {
  cursor: pointer;
  flex: 1;
}

.playlist-item:hover {
  background: #1e1e1e;
  border-radius: 5px;
}
.queue-menu {
  position: absolute;
  background: #222;
  border-radius: 8px;
  padding: 8px;
  display: none;
  flex-direction: column;
  z-index: 100000;
  width: 160px;
  animation: fadeIn 0.15s ease;
}
.queue-menu button {
  background: none;
  border: none;
  color: white;
  padding: 8px;
  text-align: left;
  cursor: pointer;
}

.queue-menu button:hover {
  background: #333;
}

@keyframes fadeIn {
  from { opacity: 0; transform: scale(0.95); }
  to { opacity: 1; transform: scale(1); }
}
.now-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
/* default */
.main {
  transition: margin-right 0.3s ease;
}

/* when queue opens */
body.queue-open .main {
  margin-right: 320px; /* same width as queue */
}
.player {
  transition: width 0.3s ease;
}

body.queue-open .player {
  width: calc(100% - 300px);
}
.next-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
</head>

<body>
  

<div class="app">

  <!-- Sidebar -->
  <div class="sidebar">
  <button onclick="showHome()" class="nav-btn">🏠</button>
  <button onclick="showSearch()" class="nav-btn">🔍</button>
  <button onclick="showFavorites()" class="nav-btn">❤️</button>
  <button onclick="createPlaylist()" class="nav-btn">➕</button>
  <div id="playlistContainer"></div>
</div>
  <!-- Main -->
  <div class="main">

    <!-- Top -->
    <div class="topbar">
      <input type="text" id="searchInput" placeholder="Search..." oninput="filterSongs()">
      <div>👤 Chirayu</div>
    </div>
    <!-- Playlist -->
    <h2 id="playlistTitle">All Songs</h2>
    <ul id="playlist"></ul>

    <!-- Cards -->
    <div class="cards">
      <div class="card" onclick="playSong(0)">
        <p>Play First Song</p>
      </div>
    </div>

  </div>
</div>

<div class="player">

  <!-- LEFT -->
<div class="left">
  <div>
    <div id="nowPlaying">No song playing</div>
    <div class="artist">Unknown</div>
  </div>
</div>

  <!-- CENTER -->
  <div class="center">

    <div class="top-controls">
      <button id="shuffleBtn" onclick="toggleShuffle()">🔀</button>
      <button onclick="prevSong()">⏮</button>
      <button id="playBtn" onclick="togglePlay()">▶</button>
      <button onclick="nextSong()">⏭</button>
      <button id="loopBtn" onclick="toggleLoop()">🔁</button>
    </div>

    <div class="progress-container">
      <span id="currentTime">0:00</span>

      <input type="range" id="progress" min="0" max="100" value="0"
             onchange="seekSong(this.value)">

      <span id="totalTime">0:00</span>
    </div>

  </div>

  <!-- RIGHT -->
  <div class="right">
    <button onclick="toggleQueue()">📋</button>
    🔊
    <input type="range" min="0" max="1" step="0.1"
           onchange="setVolume(this.value)">
  </div>

</div>
<script>
let songs = [];
let playlists = JSON.parse(localStorage.getItem("playlists")) || [];
let currentPlaylist = null;
let favorites = JSON.parse(localStorage.getItem("favorites")) || [];
let queue = [];
let audio = new Audio();
let currentIndex = 0;
let isPlaying = false;
let isShuffle = false;
let loopMode = 0;
let currentSong = null;
audio.onplay = () => {
  document.getElementById("playBtn").innerText = "⏸";
};

audio.onpause = () => {
  document.getElementById("playBtn").innerText = "▶";
};
audio.onended = () => {

  // 🔁 LOOP ONE
  if(loopMode === 2){
    audio.currentTime = 0;
    audio.play();
    return;
  }

  // 🔀 SHUFFLE
  if(isShuffle){
    let randomIndex = Math.floor(Math.random() * songs.length);
    playSong(randomIndex);
    return;
  }

  // ✅ USE YOUR QUEUE SYSTEM
  nextSong();
};
function formatTime(sec){
  let m = Math.floor(sec / 60);
  let s = Math.floor(sec % 60);
  return m + ":" + (s < 10 ? "0" + s : s);
}

async function loadSongs() {
  let res = await fetch("http://localhost:3000/songs");
  songs = await res.json();
  render();
}
function toggleQueue(){
  let panel = document.getElementById("queuePanel");
  let player = document.querySelector(".player");

  panel.classList.toggle("active");
  player.classList.toggle("shifted");
  document.body.classList.toggle("queue-open");

  // 🔥 ADD THIS LINE
  renderQueueUI();
}
async function addSong(){
  await fetch("http://localhost:3000/songs", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({
      title: "New Song",
      artist: "You",
      url: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3"
    })
  });

  loadSongs();
  
}
async function deleteSong(i){
  let id = songs[i].id;

  await fetch(`http://localhost:3000/songs/${id}`, {
    method: "DELETE"
  });

  loadSongs();
}

// Shuffle
function shuffle(){
  songs.sort(()=>Math.random()-0.5);
  render();
}

function render(){
  document.getElementById("playlistTitle").innerText = "All Songs";
  let ul = document.getElementById("playlist");
  ul.innerHTML = "";

  songs.forEach((s,i)=>{
    let li = document.createElement("li");

    if(i === currentIndex){
      li.classList.add("active");
    }

    li.innerHTML = `
  <div class="left-part">
    <span class="index">
      <span class="num">${i+1}</span>
      <span class="play-hover" onclick="playSong(${i})">▶</span>
    </span>

    <span class="song-info" onclick="playSong(${i})">
     <b class="${favorites.includes(s.id) ? 'liked-song' : ''}">
  ${s.title}
</b>
    </span>
  </div>

  <button onclick="openPlaylistMenu(${i})">➕</button>
`;

    ul.appendChild(li);
  });
}
function renderFiltered(list){
  let ul = document.getElementById("playlist");
  ul.innerHTML = "";

  list.forEach((s,i)=>{

    let originalIndex = songs.indexOf(s); // needed for play

    let li = document.createElement("li");

    li.innerHTML = `
      <div class="left-part">
        <span class="index">${i+1}</span>

        <span class="song-info" onclick="playSong(${originalIndex})">
          <b class="liked-song">${s.title}</b> - ${s.artist}
        </span>
      </div>

      <div class="actions">
        <button onclick="removeFromPlaylist(${i})">🗑️</button>
      </div>
    `;

    ul.appendChild(li);
  });
}
function renderQueueUI(){

  let current = currentSong;

  document.getElementById("qTitle").innerText = current?.title || "No song";
  document.getElementById("qArtist").innerText = current?.artist || "Unknown";

  let ul = document.getElementById("queueListUI");
  ul.innerHTML = "";

  // 🔥 1. QUEUE SONGS
  queue.forEach((s, i)=>{

    let li = document.createElement("li");

    li.innerHTML = `
      <div>
        <div>${s.title}</div>
        <div style="font-size:12px;color:#aaa">${s.artist}</div>
      </div>

      <button onclick="removeFromQueue(event, ${i})">❌</button>
    `;

    li.onclick = () => {
      let index = songs.findIndex(song => song.id === s.id);
      playSong(index);
    };

    ul.appendChild(li);
  });
  

  // 🔥 2. DEFAULT NEXT SONGS
  for(let i = currentIndex + 1; i < songs.length; i++){

    let s = songs[i];

    if(queue.some(q => q.id === s.id)) continue;

    let li = document.createElement("li");
    let isCurrent = (songs[currentIndex].id === s.id);

    li.innerHTML = `
      <div>
        <div>${s.title}</div>
        <div style="font-size:12px;color:#aaa">${s.artist}</div>
      </div>

    <button class="queue-btn" data-index="${i}">
  ${isCurrent ? "➕" : "⋯"}
</button>
    `;

    li.onclick = () => playSong(i);

    ul.appendChild(li);
    let btn = li.querySelector(".queue-btn");

btn.onclick = (e) => {
  e.stopPropagation();

  if(isCurrent){
    openPlaylistMenu(i);
  } else {
    openQueueMenu(e, i);
  }
};
  }
  
}

function playSong(i){
  currentIndex = i;
  currentSong = songs[i];   // ✅ ADD THIS

  audio.src = songs[i].url;
  audio.play();

  updateUI();
  renderQueueUI();
}
function toggleLoop(){
  loopMode = (loopMode + 1) % 3;

  let btn = document.getElementById("loopBtn");

  if(loopMode === 0){
    btn.innerText = "🔁";
    btn.classList.remove("active");
  }
  else if(loopMode === 1){
    btn.innerText = "🔁";
    btn.classList.add("active");
  }
  else{
    btn.innerText = "🔂";
    btn.classList.add("active");
  }
}
function toggleShuffle(){
  isShuffle = !isShuffle;

  let btn = document.getElementById("shuffleBtn");
  btn.classList.toggle("active", isShuffle);
}
function togglePlay(){
  if(!audio.src){
    alert("Select a song first!");
    return;
  }

  if(audio.paused){
    audio.play();
  } else {
    audio.pause();
  }
}

// Next
function nextSong(){

  // ✅ PLAY FROM QUEUE FIRST
  if(queue.length > 0){
    let next = queue.shift(); // remove first

    let index = songs.findIndex(s => s.id === next.id);

    if(index !== -1){
      playSong(index);
    }

    return;
  }

  // ✅ NORMAL FLOW
  currentIndex = (currentIndex + 1) % songs.length;
  playSong(currentIndex);
}

// Previous
function prevSong(){
  currentIndex = (currentIndex - 1 + songs.length) % songs.length;
  playSong(currentIndex);
}
function toggleFavorite(i){
  let id = songs[i].id;

  if(favorites.includes(id)){
    favorites = favorites.filter(f => f !== id);
  } else {
    favorites.push(id);
  }
  localStorage.setItem("favorites", JSON.stringify(favorites));

  render(); // refresh UI
  
}
function createPlaylist(){
  let name = prompt("Enter playlist name:");

  if(!name) return;

  let newPlaylist = {
    name: name,
    songs: []
  };

  playlists.push(newPlaylist);

  localStorage.setItem("playlists", JSON.stringify(playlists));

  renderPlaylists();
}
function renderPlaylists(){
  let container = document.getElementById("playlistContainer");
  container.innerHTML = "";

  if(playlists.length === 0){
    container.innerHTML = `<p style="color:#888;font-size:12px;">No playlists yet</p>`;
    return;
  }

  playlists.forEach((p, index)=>{
    let div = document.createElement("div");

    div.innerHTML = `
      <span onclick="openPlaylist(${index})">${p.name}</span>
      <button onclick="deletePlaylist(${index})">🗑️</button>
    `;

    div.className = "playlist-item";

    container.appendChild(div);
  });
}
function addToPlaylist(i){
  if(currentPlaylist === null){
    alert("Open a playlist first!");
    return;
  }

  let song = songs[i];

  playlists[currentPlaylist].songs.push(song);

  localStorage.setItem("playlists", JSON.stringify(playlists));

  alert("Added to playlist!");
}
function openPlaylist(index){
  currentPlaylist = index;

  let list = playlists[index].songs;

  renderFiltered(list);
}
function updateUI(){

  let song = currentSong || songs[currentIndex];

  // ✅ MAIN PLAYER
  document.getElementById("nowPlaying").innerText =
    song?.title || "No song";

  document.querySelector(".artist").innerText =
    song?.artist || "Unknown";

  // ✅ QUEUE PANEL
  document.getElementById("qTitle").innerText =
    song?.title || "No song";

  document.getElementById("qArtist").innerText =
    song?.artist || "Unknown";
}
function setVolume(val){
  audio.volume = val;
}
// Progress
audio.ontimeupdate = ()=>{
  let progress = document.getElementById("progress");
  progress.value = (audio.currentTime / audio.duration) * 100 || 0;

  document.getElementById("currentTime").innerText =
    formatTime(audio.currentTime);

  document.getElementById("totalTime").innerText =
    formatTime(audio.duration || 0);
};

// Seek
function seekSong(val){
  audio.currentTime = (val/100)*audio.duration;
}
loadSongs();
renderPlaylists();   // ✅ ADD THIS
function showHome(){
  render();
  setActive(0);
}

function showSearch(){
  document.querySelector(".search").focus();
  setActive(1);
}

function showFavorites(){
  let favSongs = songs.filter(s => favorites.includes(s.id));
  renderFiltered(favSongs);
  setActive(2);
}
function setActive(index){
  let btns = document.querySelectorAll(".nav-btn");
  btns.forEach(b => b.classList.remove("active"));
  btns[index].classList.add("active");
}
let selectedSongIndex = null;

function openPlaylistMenu(i){
  selectedSongIndex = i;

  let modal = document.getElementById("playlistModal");
  let list = document.getElementById("playlistList");

  list.innerHTML = "";

  // 🔥 SET FAVORITE BUTTON TEXT
  let favBtn = document.getElementById("favBtn");

  if(favorites.includes(songs[i].id)){
    favBtn.innerText = "💔 Remove from Favorites";
  } else {
    favBtn.innerText = "❤️ Add to Favorites";
  }

  // playlist buttons
  playlists.forEach((p, index)=>{
    let btn = document.createElement("button");
    btn.innerText = p.name;

    btn.onclick = () => {
      playlists[index].songs.push(songs[i]);
      localStorage.setItem("playlists", JSON.stringify(playlists));
      closeModal();
      renderPlaylists();
    };

    list.appendChild(btn);
  });

  modal.style.display = "flex";
}
function createPlaylistFromMenu(){
  let name = prompt("Enter playlist name:");
  if(!name) return;

  let newPlaylist = { name, songs: [] };

  playlists.push(newPlaylist);

  // auto add selected song
  newPlaylist.songs.push(songs[selectedSongIndex]);

  localStorage.setItem("playlists", JSON.stringify(playlists));

  closeModal();
  renderPlaylists();

  alert("Playlist created & song added!");
}
function addToFavoritesFromMenu(){
  let id = songs[selectedSongIndex].id;

  if(favorites.includes(id)){
    favorites = favorites.filter(f => f !== id);
  } else {
    favorites.push(id);
  }

  localStorage.setItem("favorites", JSON.stringify(favorites));

  closeModal();
  render(); // update UI

  alert("Updated favorites!");
}
function addToQueueFromMenu(){

  let song = songs[selectedSongIndex];

  queue.push(song);

  closeModal();
  renderQueueUI();
}
let selectedQueueIndex = null;

function openQueueMenu(event, index){
  event.stopPropagation();

  selectedQueueIndex = index;

  let menu = document.getElementById("queueMenu");
  let panel = document.getElementById("queuePanel");

  let rect = event.target.getBoundingClientRect();
  let panelRect = panel.getBoundingClientRect();

  menu.style.display = "flex";

  // 🔥 THIS IS THE IMPORTANT LINE
  menu.style.top = (rect.top - panelRect.top + panel.scrollTop) + "px";

  menu.style.left = (rect.right - panelRect.left - 150) + "px";
}
function playNextFromMenu(){

  let song;

  // ✅ if clicked item is inside queue
  if(selectedQueueIndex < queue.length){
    song = queue.splice(selectedQueueIndex, 1)[0];
  }
  else{
    // ✅ clicked from default songs
    let index = selectedQueueIndex;
    song = songs[index];
  }

  // remove duplicate if already exists
  queue = queue.filter(q => q.id !== song.id);

  // add to front
  queue.unshift(song);

  renderQueueUI();
  closeQueueMenu();
}
function removeFromQueueMenu(){

  // ✅ Only remove if it's from queue
  if(selectedQueueIndex < queue.length){
    queue.splice(selectedQueueIndex, 1);
  }

  renderQueueUI();
  closeQueueMenu();
}
// ✅ CLOSE MODAL FUNCTION (MISSING IN YOUR CODE)
function closeModal(){
  document.getElementById("playlistModal").style.display = "none";
}function closeQueueMenu(){
  let menu = document.getElementById("queueMenu");
  if(menu){
    menu.style.display = "none";
  }
}

// ✅ CLICK OUTSIDE TO CLOSE MENU
window.addEventListener("click", function(e){
  let menu = document.getElementById("queueMenu");

  if(menu && !menu.contains(e.target)){
    closeQueueMenu();
  }
});

// ✅ CLICK OUTSIDE TO CLOSE
window.onclick = function(e){
  let modal = document.getElementById("playlistModal");

  if(e.target === modal){
    closeModal();
  }
};
function removeFromPlaylist(i){

  if(currentPlaylist === null){
    alert("No playlist selected");
    return;
  }

  // remove that song from selected playlist
  playlists[currentPlaylist].songs.splice(i, 1);

  // save
  localStorage.setItem("playlists", JSON.stringify(playlists));

  // re-render playlist
  openPlaylist(currentPlaylist);
}
function removeFromQueue(event, i){
  event.stopPropagation(); // 🔥 THIS FIXES IT

  queue.splice(i, 1);
  renderQueueUI();
}
function addToQueueDirect(event, i){
  event.stopPropagation();

  let song = songs[i];

  // avoid duplicate
  if(queue.some(q => q.id === song.id)){
    return;
  }

  queue.push(song);

  renderQueueUI();
}
function addQueueSongToPlaylist(){

  let song;

  // ✅ from queue
  if(selectedQueueIndex < queue.length){
    song = queue[selectedQueueIndex];
  }
  else{
    // ✅ from normal list
    song = songs[selectedQueueIndex];
  }

  // 🔥 convert to real index
  let realIndex = songs.findIndex(s => s.id === song.id);

  selectedSongIndex = realIndex;

  openPlaylistMenu(realIndex);

  closeQueueMenu();
}
function filterSongs(){

  let query = document.getElementById("searchInput").value.toLowerCase();

  if(query === ""){
    render(); // ✅ FIXED
    return;
  }

  let filteredSongs = songs.filter(song =>
    song.title.toLowerCase().includes(query) ||
    song.artist.toLowerCase().includes(query)
  );

  renderFilteredSongs(filteredSongs);
}
function renderFilteredSongs(list){

  let container = document.getElementById("playlist"); // your songs container
  container.innerHTML = "";

  list.forEach((song, i) => {

    let originalIndex = songs.findIndex(s => s.id === song.id);

    container.innerHTML += `
      <div class="song" onclick="playSong(${originalIndex})">
        <span>${originalIndex + 1}</span>
        <span style="color:${favorites.includes(song.id) ? 'hotpink' : '#4cc9f0'}">
          ${song.title}
        </span>

        <button onclick="event.stopPropagation(); openPlaylistMenu(${originalIndex})">➕</button>
      </div>
    `;
  });
}
</script>
<div id="queuePanel" class="queue-panel">

  <div class="queue-header">
    <span>Queue</span>
    <button onclick="toggleQueue()">✖</button>
  </div>

  <div class="now-playing">
    <h3>Now playing</h3>

   <div class="now-card">

  <div class="text">
    <div id="qTitle">No song</div>
    <div id="qArtist">Unknown</div>
  </div>



</div>
  <div class="next-list">
    <h3>Next</h3>
    <ul id="queueListUI"></ul>
  </div>

</div>
<div id="playlistModal" class="modal">
  <div class="modal-content">
    <h3>Select Option</h3>

    <!-- ✅ ADD THIS -->
    <button id="favBtn" onclick="addToFavoritesFromMenu()"></button>
    <button onclick="addToQueueFromMenu()">📥 Add to Queue</button>
    <div id="playlistList"></div>

    <button onclick="createPlaylistFromMenu()">➕ Create New Playlist</button>
    <button onclick="closeModal()">Close</button>
  </div>
</div>
<div id="queueMenu" class="queue-menu">
  <button onclick="playNextFromMenu()">▶ Play Next</button>
  <button onclick="removeFromQueueMenu()">❌ Remove from Queue</button>
  <button onclick="addQueueSongToPlaylist()">📁 Add to Playlist</button>
</div>
</body>
</html>
