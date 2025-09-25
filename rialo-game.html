<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Rialo Explorer</title>
  <style>
    body { margin: 0; overflow: hidden; background: #111; }
    #scoreboard {
      position: fixed;
      top: 10px;
      left: 10px;
      color: white;
      font-size: 18px;
      font-family: Arial, sans-serif;
      background: rgba(0,0,0,0.5);
      padding: 8px 12px;
      border-radius: 6px;
    }
    #message {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      color: yellow;
      font-size: 16px;
      background: rgba(0,0,0,0.6);
      padding: 6px 12px;
      border-radius: 6px;
      display: none;
    }
  </style>
</head>
<body>
  <div id="scoreboard">Rialo Points: 0</div>
  <div id="message"></div>

  <script src="https://cdn.jsdelivr.net/npm/three@0.161.0/build/three.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/three@0.161.0/examples/js/controls/PointerLockControls.js"></script>

  <script>
    // --- Сцена ---
    const scene = new THREE.Scene();
    scene.background = new THREE.Color(0x222222);

    // Камера
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0, 1.6, 5);

    // Рендерер
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // Контроли
    const controls = new THREE.PointerLockControls(camera, document.body);
    document.body.addEventListener('click', () => controls.lock());

    // Освітлення
    const light = new THREE.DirectionalLight(0xffffff, 1);
    light.position.set(10, 10, 10);
    scene.add(light);
    scene.add(new THREE.AmbientLight(0x404040));

    // Земля
    const ground = new THREE.Mesh(
      new THREE.PlaneGeometry(100, 100),
      new THREE.MeshPhongMaterial({ color: 0x228833 })
    );
    ground.rotation.x = -Math.PI / 2;
    scene.add(ground);

    // --- Ресурси ---
    const resourceNodes = [];
    const resourceGroup = new THREE.Group();
    scene.add(resourceGroup);

    function spawnResource(x, z) {
      const geo = new THREE.BoxGeometry(1, 1, 1);
      const mat = new THREE.MeshPhongMaterial({ color: 0x8844ff });
      const cube = new THREE.Mesh(geo, mat);
      cube.position.set(x, 0.5, z);
      cube.userData.isDestroying = false;
      resourceGroup.add(cube);
      resourceNodes.push(cube);
    }
    for (let i = 0; i < 20; i++) {
      spawnResource((Math.random() - 0.5) * 50, (Math.random() - 0.5) * 50);
    }

    // --- Стан гри ---
    let score = 0;
    const scoreboard = document.getElementById("scoreboard");
    const message = document.getElementById("message");

    function flashMessage(text) {
      message.innerText = text;
      message.style.display = "block";
      setTimeout(() => { message.style.display = "none"; }, 1500);
    }

    // --- Частинки (спаркси) ---
    function spawnParticles(position, color = 0xaa44ff) {
      const particles = [];
      const geo = new THREE.SphereGeometry(0.05, 6, 6);
      const mat = new THREE.MeshBasicMaterial({ color });

      for (let i = 0; i < 15; i++) {
        const p = new THREE.Mesh(geo, mat.clone());
        p.position.copy(position);
        p.userData.velocity = new THREE.Vector3(
          (Math.random() - 0.5) * 2,
          Math.random() * 2,
          (Math.random() - 0.5) * 2
        );
        p.userData.life = 1.0;
        scene.add(p);
        particles.push(p);
      }
      activeParticles.push(...particles);
    }

    const activeParticles = [];

    function updateParticles(delta) {
      for (let i = activeParticles.length - 1; i >= 0; i--) {
        const p = activeParticles[i];
        p.position.addScaledVector(p.userData.velocity, delta);
        p.userData.velocity.multiplyScalar(0.95);
        p.userData.life -= delta;
        p.material.opacity = Math.max(0, p.userData.life);
        if (p.userData.life <= 0) {
          scene.remove(p);
          activeParticles.splice(i, 1);
        }
      }
    }

    // --- Управління ---
    const keys = {};
    window.addEventListener('keydown', e => keys[e.code] = true);
    window.addEventListener('keyup', e => keys[e.code] = false);

    function gatherResource() {
      let closest = null, dist = 2;
      for (let node of resourceNodes) {
        if (node.userData.isDestroying) continue;
        const d = camera.position.distanceTo(node.position);
        if (d < dist) { dist = d; closest = node; }
      }
      if (closest) {
        closest.userData.isDestroying = true;
        flashMessage("Resource Collected!");
        score += 5;
        scoreboard.innerText = "Rialo Points: " + score;
        spawnParticles(closest.position);
      }
    }

    function craftToken() {
      if (score >= 5) {
        score += 10;
        scoreboard.innerText = "Rialo Points: " + score;
        flashMessage("Crafted Rialo Token!");
      } else {
        flashMessage("Not enough resources!");
      }
    }

    window.addEventListener('keydown', e => {
      if (e.code === 'KeyE') gatherResource();
      if (e.code === 'KeyC') craftToken();
    });

    // --- Рух ---
    const velocity = new THREE.Vector3();
    const direction = new THREE.Vector3();
    const moveSpeed = 5.0;

    function move(delta) {
      direction.set(0, 0, 0);
      if (keys["KeyW"]) direction.z -= 1;
      if (keys["KeyS"]) direction.z += 1;
      if (keys["KeyA"]) direction.x -= 1;
      if (keys["KeyD"]) direction.x += 1;

      direction.normalize();
      velocity.copy(direction).applyQuaternion(camera.quaternion).multiplyScalar(moveSpeed * delta);

      controls.getObject().position.add(velocity);
    }

    // --- Resize ---
    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    // --- Цикл ---
    const clock = new THREE.Clock();
    function animate() {
      requestAnimationFrame(animate);
      const delta = clock.getDelta();

      // Анімація руйнування кубів
      for (let i = resourceNodes.length - 1; i >= 0; i--) {
        const node = resourceNodes[i];
        if (node.userData.isDestroying) {
          node.scale.multiplyScalar(0.85);
          if (node.scale.x < 0.1) {
            resourceGroup.remove(node);
            resourceNodes.splice(i, 1);
          }
        }
      }

      // Оновлення частинок
      updateParticles(delta);

      if (controls.isLocked) move(delta);
      renderer.render(scene, camera);
    }
    animate();
  </script>
</body>
</html>
