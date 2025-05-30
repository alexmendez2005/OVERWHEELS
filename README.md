# OVERWHEELS
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Overwheels - Menú Principal</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to right, #1f1f1f, #2a2a2a);
      color: #fff;
      text-align: center;
      padding: 40px;
    }
    h1 {
      font-size: 48px;
      margin-bottom: 20px;
      color: #f9c300;
    }
    select, button {
      padding: 12px;
      margin: 10px;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    select {
      background-color: #333;
      color: #fff;
    }
    button {
      background-color: #f9c300;
      color: #000;
      transition: background 0.3s;
    }
    button:hover {
      background-color: #ffe25a;
    }
    .panel {
      background-color: #292929;
      padding: 20px;
      border-radius: 12px;
      max-width: 600px;
      margin: auto;
      box-shadow: 0 0 15px #000;
    }
    .log {
      background: #111;
      color: #0f0;
      font-family: monospace;
      font-size: 14px;
      padding: 10px;
      text-align: left;
      max-height: 200px;
      overflow-y: auto;
      margin-top: 20px;
      border-radius: 8px;
    }
  </style>
</head>
<body>

  <div class="panel">
    <h1>Overwheels</h1>

    <label for="language">🌐 Idioma / Language:</label><br>
    <select id="language">
      <option value="EN">English</option>
      <option value="ES">Español</option>
      <option value="JA">日本語</option>
      <option value="ID">Bahasa Indonesia</option>
      <option value="ZH">中文</option>
    </select>

    <br><br>
    <label for="city">🌆 Ciudad:</label><br>
    <select id="city">
      <option>Wolverine Hills</option>
      <option>Los Belitos</option>
      <option>Anstadt</option>
      <option>Neon Bay</option>
      <option>Savannah Cross</option>
      <option>Ironport</option>
      <option>Royal Mirage</option>
    </select>

    <br><br>
    <button onclick="loadCity()">Cargar Ciudad</button>
    <button onclick="toggleEditor()">Editor de Niveles</button>
    <button onclick="startMultiplayer()">Multijugador Local</button>
    <br><br>
    <button onclick="goToInstagram()">Instagram</button>

    <div class="log" id="log"></div>

    <p style="margin-top: 20px; font-size: 14px; color: #aaa;">
      © 2023 Alexander, Argentina. Todos los derechos reservados.<br>
      Overwheels™ es una marca registrada.
    </p>
  </div>

  <script>
    const logEl = document.getElementById("log");
    const translations = {
      EN: { load: "Loading city", editor: "Level editor activated", multiplayer: "Starting local multiplayer..." },
      ES: { load: "Cargando ciudad", editor: "Editor de niveles activado", multiplayer: "Iniciando partida local..." },
      JA: { load: "都市を読み込み中", editor: "レベルエディターを起動", multiplayer: "ローカルマルチプレイヤーを開始中..." },
      ID: { load: "Memuat kota", editor: "Editor level diaktifkan", multiplayer: "Memulai multipemain lokal..." },
      ZH: { load: "加载城市", editor: "关卡编辑器已激活", multiplayer: "正在启动本地多人游戏..." }
    };

    function getLang() {
      return document.getElementById("language").value;
    }

    function log(msg) {
      const p = document.createElement("div");
      p.textContent = "> " + msg;
      logEl.appendChild(p);
      logEl.scrollTop = logEl.scrollHeight;
    }

    function loadCity() {
      const city = document.getElementById("city").value;
      log(`${translations[getLang()].load}: ${city.replace(" ", "_")}`);
    }

    function toggleEditor() {
      log(translations[getLang()].editor);
    }

    function startMultiplayer() {
      log(translations[getLang()].multiplayer);
    }

    function goToInstagram() {
      window.open("https://instagram.com/7alex.07", "_blank");
    }
  </script>

</body>
</html>
<?xml version="1.0" encoding="UTF-8"?>
<resources>
    <!-- English -->
    <string name="play">PLAY</string>
    <string name="credits">CREDITS</string>
    
    <!-- Spanish -->
    <string name="play_es">JUGAR</string>
    <string name="credits_es">CRÉDITOS</string>
    
    <!-- Japanese -->
    <string name="play_ja">プレイ</string>
    <string name="credits_ja">クレジット</string>
    
    <!-- Indonesian -->
    <string name="play_id">MAINKAN</string>
    <string name="credits_id">KREDIT</string>
    
    <!-- Chinese -->
    <string name="play_zh">玩</string>
    <string name="credits_zh">学分</string>
</resources>
File > Build Settings > Android:
- Texture Compression: ASTC
- Minimum API Level: Android 9.0 (Pie)
- Target Architecture: ARMv7 + ARM64
#!/bin/bash
UNITY_PATH="/Applications/Unity/Hub/Editor/2021.3.11f1/Unity.app/Contents/MacOS/Unity"
PROJECT_PATH="/Users/tuusuario/Overwheels"
APK_OUTPUT="$PROJECT_PATH/Builds/Overwheels.apk"

$UNITY_PATH -quit -batchmode -projectPath $PROJECT_PATH \
-buildTarget Android -executeMethod BuildScript.BuildAPK \
-outputPath $APK_OUTPUT
using UnityEditor;
using UnityEngine;

public class BuildScript
{
    [MenuItem("Build/Build APK")]
    public static void BuildAPK()
    {
        BuildPlayerOptions options = new BuildPlayerOptions();
        options.scenes = new[] { 
            "Assets/Scenes/MainMenu.unity", 
            "Assets/Scenes/Wolverine_Hills.unity" 
        };
        options.locationPathName = "Builds/Overwheels.apk";
        options.target = BuildTarget.Android;
        options.options = BuildOptions.CompressWithLz4HC;
        
        BuildPipeline.BuildPlayer(options);
    }
}
