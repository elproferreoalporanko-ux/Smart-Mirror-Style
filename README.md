
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Espejo Inteligente - Asesor de Ropa</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <header>
            <h1>🪞 Espejo Inteligente</h1>
            <p>Asesor de Ropa con IA</p>
        </header>

        <div class="main-content">
            <!-- Sección de Cámara -->
            <div class="camera-section">
                <div class="camera-container">
                    <video id="videoStream" autoplay playsinline></video>
                    <canvas id="canvas" style="display: none;"></canvas>
                </div>
                <div class="camera-controls">
                    <button id="startBtn" class="btn btn-primary">📹 Iniciar Cámara</button>
                    <button id="captureBtn" class="btn btn-success" disabled>📸 Capturar Foto</button>
                    <button id="stopBtn" class="btn btn-danger" disabled>⏹️ Detener</button>
                </div>
            </div>

            <!-- Sección de Recomendaciones -->
            <div class="recommendations-section">
                <div class="photo-preview">
                    <h3>Foto Capturada</h3>
                    <img id="capturedPhoto" src="" alt="Foto capturada" style="display: none;">
                    <p id="noPhotoText" class="no-photo">Sin foto capturada</p>
                </div>

                <div class="ai-recommendations">
                    <h3>🤖 Recomendaciones de IA</h3>
                    <div id="loadingSpinner" class="spinner" style="display: none;"></div>
                    <div id="recommendations" class="recommendations-content">
                        <p class="placeholder">Captura una foto para obtener recomendaciones de ropa</p>
                    </div>
                </div>
            </div>
        </div>

        <footer>
            <p>Espejo Inteligente v1.0 | Asesor de Ropa con IA</p>
        </footer>
    </div>

    <script src="script.js"></script>
</body>
</html>

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    color: #333;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

header {
    text-align: center;
    color: white;
    margin-bottom: 30px;
    padding: 20px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 15px;
    backdrop-filter: blur(10px);
}

header h1 {
    font-size: 2.5rem;
    margin-bottom: 10px;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

header p {
    font-size: 1.2rem;
    opacity: 0.9;
}

.main-content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    flex: 1;
    margin-bottom: 30px;
}

/* SECCIÓN DE CÁMARA */
.camera-section {
    background: white;
    border-radius: 15px;
    padding: 20px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
    display: flex;
    flex-direction: column;
}

.camera-container {
    position: relative;
    width: 100%;
    aspect-ratio: 4 / 3;
    background: #000;
    border-radius: 10px;
    overflow: hidden;
    margin-bottom: 15px;
}

#videoStream {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transform: scaleX(-1);
}

.camera-controls {
    display: flex;
    gap: 10px;
    justify-content: center;
    flex-wrap: wrap;
}

/* BOTONES */
.btn {
    padding: 12px 24px;
    border: none;
    border-radius: 8px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.btn:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}

.btn-primary {
    background: #667eea;
    color: white;
}

.btn-primary:hover:not(:disabled) {
    background: #5568d3;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

.btn-success {
    background: #48bb78;
    color: white;
}

.btn-success:hover:not(:disabled) {
    background: #38a169;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(72, 187, 120, 0.4);
}

.btn-danger {
    background: #f56565;
    color: white;
}

.btn-danger:hover:not(:disabled) {
    background: #e53e3e;
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(245, 101, 101, 0.4);
}

/* SECCIÓN DE RECOMENDACIONES */
.recommendations-section {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.photo-preview {
    background: white;
    border-radius: 15px;
    padding: 20px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
}

.photo-preview h3,
.ai-recommendations h3 {
    color: #667eea;
    margin-bottom: 15px;
    font-size: 1.3rem;
}

#capturedPhoto {
    width: 100%;
    border-radius: 10px;
    max-height: 300px;
    object-fit: cover;
}

.no-photo {
    text-align: center;
    color: #999;
    padding: 40px 20px;
    font-style: italic;
}

.ai-recommendations {
    background: white;
    border-radius: 15px;
    padding: 20px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
    flex: 1;
    overflow-y: auto;
    max-height: 400px;
}

.recommendations-content {
    line-height: 1.8;
}

.placeholder {
    text-align: center;
    color: #999;
    padding: 30px 20px;
    font-style: italic;
}

.recommendation-item {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 15px;
    border-radius: 10px;
    margin-bottom: 15px;
}

.recommendation-item h4 {
    margin-bottom: 8px;
    font-size: 1.1rem;
}

.recommendation-item p {
    font-size: 0.95rem;
    opacity: 0.95;
}

.recommendation-item ul {
    margin-left: 20px;
    margin-top: 10px;
}

.recommendation-item li {
    margin-bottom: 5px;
}

/* SPINNER DE CARGA */
.spinner {
    display: inline-block;
    width: 40px;
    height: 40px;
    border: 4px solid #f3f3f3;
    border-top: 4px solid #667eea;
    border-radius: 50%;
    animation: spin 1s linear infinite;
    margin: 20px auto;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

/* FOOTER */
footer {
    text-align: center;
    color: white;
    padding: 20px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 15px;
    backdrop-filter: blur(10px);
}

/* RESPONSIVE */
@media (max-width: 768px) {
    .main-content {
        grid-template-columns: 1fr;
    }

    header h1 {
        font-size: 1.8rem;
    }

    .camera-controls {
        flex-direction: column;
    }

    .btn {
        width: 100%;
    }

    .ai-recommendations {
        max-height: 500px;
    }
}

// ============================================
// ESPEJO INTELIGENTE - ASESOR DE ROPA CON IA
// ============================================

const videoStream = document.getElementById('videoStream');
const canvas = document.getElementById('canvas');
const capturedPhoto = document.getElementById('capturedPhoto');
const noPhotoText = document.getElementById('noPhotoText');
const recommendations = document.getElementById('recommendations');
const loadingSpinner = document.getElementById('loadingSpinner');

const startBtn = document.getElementById('startBtn');
const captureBtn = document.getElementById('captureBtn');
const stopBtn = document.getElementById('stopBtn');

let stream = null;
let currentImageData = null;

// ============================================
// 1. INICIAR CÁMARA
// ============================================
startBtn.addEventListener('click', async () => {
    try {
        stream = await navigator.mediaDevices.getUserMedia({
            video: { facingMode: 'environment', width: { ideal: 1280 }, height: { ideal: 720 } }
        });
        videoStream.srcObject = stream;
        
        startBtn.disabled = true;
        captureBtn.disabled = false;
        stopBtn.disabled = false;
        
        console.log('✅ Cámara iniciada');
    } catch (error) {
        alert('Error al acceder a la cámara: ' + error.message);
        console.error('Error:', error);
    }
});

// ============================================
// 2. CAPTURAR FOTO
// ============================================
captureBtn.addEventListener('click', () => {
    const context = canvas.getContext('2d');
    canvas.width = videoStream.videoWidth;
    canvas.height = videoStream.videoHeight;
    
    // Flip horizontalmente (espejo)
    context.scale(-1, 1);
    context.drawImage(videoStream, -canvas.width, 0, canvas.width, canvas.height);
    
    // Convertir a imagen
    currentImageData = canvas.toDataURL('image/jpeg');
    capturedPhoto.src = currentImageData;
    capturedPhoto.style.display = 'block';
    noPhotoText.style.display = 'none';
    
    console.log('📸 Foto capturada');
    
    // Obtener recomendaciones
    getRecommendations();
});

// ============================================
// 3. DETENER CÁMARA
// ============================================
stopBtn.addEventListener('click', () => {
    if (stream) {
        stream.getTracks().forEach(track => track.stop());
        stream = null;
    }
    videoStream.srcObject = null;
    
    startBtn.disabled = false;
    captureBtn.disabled = true;
    stopBtn.disabled = true;
    
    console.log('⏹️ Cámara detenida');
});

// ============================================
// 4. ANÁLISIS DE ROPA CON IA BÁSICA
// ============================================
async function analyzeClothing(imageData) {
    // IA BÁSICA - Análisis sin API externa
    // En un futuro puedes integrar OpenAI o Google Vision
    
    return new Promise((resolve) => {
        setTimeout(() => {
            const recommendations = generateAIRecommendations();
            resolve(recommendations);
        }, 2000); // Simular tiempo de procesamiento
    });
}

// ============================================
// 5. GENERAR RECOMENDACIONES (IA BÁSICA)
// ============================================
function generateAIRecommendations() {
    const tipesDeRopa = {
        camisetas: [
            '👕 Camiseta de algodón',
            '👕 Camiseta de lino',
            '👕 Camiseta deportiva'
        ],
        pantalones: [
            '👖 Jeans clásicos',
            '👖 Pantalón chino',
            '👖 Pantalón deportivo'
        ],
        calzado: [
            '👟 Zapatillas deportivas',
            '👟 Zapatos casuales',
            '👟 Botas'
        ],
        accesorios: [
            '🧢 Gorra',
            '🧣 Bufanda',
            '👜 Mochila'
        ]
    };

    const cuidados = {
        algodón: 'Lavar en agua fría, secar al aire libre, planchar a temperatura media',
        lino: 'Lavar en agua tibia, puede encogerse ligeramente, planchar húmedo',
        poliéster: 'Lavar en agua fría, secadora a baja temperatura, baja necesidad de planchado',
        lana: 'Lavar a mano en agua fría, secar plano, usar champú especial para lana',
        jeans: 'Lavar del revés, agua fría, secar al aire libre, lavar cada 3-5 usos',
        deportiva: 'Lavar en agua fría, secar al aire libre, evitar secadora',
        gamuza: 'Limpiar con cepillo suave, no lavar, usar protector para gamuza',
        cuero: 'Limpiar con paño húmedo, usar acondicionador de cuero, proteger de la humedad'
    };

    const outfits = [
        {
            nombre: 'Casual Diario',
            prendas: ['Camiseta de algodón', 'Jeans clásicos', 'Zapatillas deportivas'],
            ocasion: 'Día a día',
            temperatura: 'Cualquier clima'
        },
        {
            nombre: 'Elegante',
            prendas: ['Camisa de lino', 'Pantalón chino', 'Zapatos casuales'],
            ocasion: 'Citas, eventos',
            temperatura: 'Templado'
        },
        {
            nombre: 'Deportivo',
            prendas: ['Camiseta deportiva', 'Pantalón deportivo', 'Zapatillas deportivas'],
            ocasion: 'Gym, ejercicio',
            temperatura: 'Cálido'
        },
        {
            nombre: 'Invernal',
            prendas: ['Suéter de lana', 'Pantalón oscuro', 'Botas', 'Bufanda'],
            ocasion: 'Frío extremo',
            temperatura: 'Frío'
        }
    ];

    // Seleccionar aleatoriamente
    const outfitAleatorio = outfits[Math.floor(Math.random() * outfits.length)];
    const materialesAleatorios = Object.keys(cuidados).slice(0, 3);

    const resultado = {
        outfit: outfitAleatorio,
        cuidados: materialesAleatorios.map(material => ({
            material: material,
            instrucciones: cuidados[material]
        })),
        consejos: [
            'Combina colores neutrales con acentos de color',
            'Invierte en prendas básicas de buena calidad',
            'Adapta tu outfit a la temperatura del día',
            'Considera la ocasión al elegir tu ropa',
            'Mantén tus prendas limpias y en buen estado'
        ]
    };

    return resultado;
}

// ============================================
// 6. OBTENER Y MOSTRAR RECOMENDACIONES
// ============================================
async function getRecommendations() {
    if (!currentImageData) {
        alert('Por favor captura una foto primero');
        return;
    }

    // Mostrar spinner de carga
    loadingSpinner.style.display = 'block';
    recommendations.innerHTML = '';

    try {
        // Analizar ropa en la foto
        const resultado = await analyzeClothing(currentImageData);

        // Ocultar spinner
        loadingSpinner.style.display = 'none';

        // Mostrar recomendaciones
        let html = '';

        // OUTFIT RECOMENDADO
        html += `
            <div class="recommendation-item">
                <h4>👗 Outfit Recomendado: ${resultado.outfit.nombre}</h4>
                <p><strong>Ocasión:</strong> ${resultado.outfit.ocasion}</p>
                <p><strong>Clima:</strong> ${resultado.outfit.temperatura}</p>
                <p><strong>Prendas:</strong></p>
                <ul>
                    ${resultado.outfit.prendas.map(prenda => `<li>${prenda}</li>`).join('')}
                </ul>
            </div>
        `;

        // CUIDADOS TEXTILES
        html += `<div class="recommendation-item">
            <h4>🧺 Cuidados Textiles Recomendados</h4>
        `;
        resultado.cuidados.forEach(cuidado => {
            html += `
                <p><strong>• ${cuidado.material.toUpperCase()}:</strong></p>
                <p style="margin-left: 20px; font-size: 0.9rem;">${cuidado.instrucciones}</p>
            `;
        });
        html += `</div>`;

        // CONSEJOS DE ESTILO
        html += `
            <div class="recommendation-item">
                <h4>✨ Consejos de Estilo</h4>
                <ul>
                    ${resultado.consejos.map(consejo => `<li>${consejo}</li>`).join('')}
                </ul>
            </div>
        `;

        recommendations.innerHTML = html;
        console.log('✅ Recomendaciones generadas');

    } catch (error) {
        loadingSpinner.style.display = 'none';
        recommendations.innerHTML = `<p style="color: red;">Error al procesar la foto: ${error.message}</p>`;
        console.error('Error:', error);
    }
}

// ============================================
// 7. INICIALIZACIÓN
// ============================================
console.log('🪞 Espejo Inteligente cargado correctamente');
console.log('📸 Haz clic en "Iniciar Cámara" para comenzar');
