import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';

// Scene setup
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
camera.position.set(0, 0, 5);

const renderer = new THREE.WebGLRenderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

// Add a rotating sphere
const geometry = new THREE.SphereGeometry(1, 32, 32);
const material = new THREE.MeshStandardMaterial({ color: 0x0077B5, wireframe: true });
const sphere = new THREE.Mesh(geometry, material);
scene.add(sphere);

// Light setup
const light = new THREE.PointLight(0xffffff, 1, 100);
light.position.set(5, 5, 5);
scene.add(light);

// Controls
const controls = new OrbitControls(camera, renderer.domElement);
controls.enableDamping = true;

// Resize handler
window.addEventListener('resize', () => {
  renderer.setSize(window.innerWidth, window.innerHeight);
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
});

// Animation loop
function animate() {
  requestAnimationFrame(animate);
  sphere.rotation.y += 0.01;
  controls.update();
  renderer.render(scene, camera);
}
animate();

// Add clickable text elements
document.body.innerHTML += `
  <div style="position: absolute; top: 20px; left: 50%; transform: translateX(-50%); text-align: center; color: white;">
    <h1>Hello! I'm Harshil</h1>
    <p>Web Developer | React | Node.js</p>
    <a href="https://www.linkedin.com/in/harshil-dhaduk-4b05a5251" target="_blank">LinkedIn</a>
    <a href="https://github.com/harshildhaduk01" target="_blank">GitHub</a>
  </div>
`;
