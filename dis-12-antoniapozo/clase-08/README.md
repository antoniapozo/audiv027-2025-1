# clase-08

no hay clase por interferiado.

## bitácora de proceso
//Quiero hacer 3 imágenes que aparezcan dependiendo del sonido o audio que se reproduzca
//Quiero trabajar con 2 géneros musicales y el silencio
//Primero se entrenará este modelo con los 3 sonidos

// Teachable Machine
let label = "silencio";

// Classifier y model url
let classifier;
let modelURL = 'https://teachablemachine.withgoogle.com/models/XhfJySVT6/';

//Subir la imágen que corresponde a cada comando de sonido

// Imagenes
let imgNeutral;
let imgJazz;
let imgReggaeton;

//Aquí se carga el modelo con el clasificador del sonido

function preload() {
  classifier = ml5.soundClassifier(modelURL + 'model.json');
  
  // Cargar  imagenes
  imgNeutral = loadImage('neutral.png');       // Para "silencio"
  imgJazz = loadImage('Jazz.png');             // Para "Jazz"
  imgReggaeton = loadImage('Reggaetón.png');   // Para "Reggaetón"
}

function setup() {
  createCanvas(300, 400);
  imageMode(CENTER); // Para centrar imagenes
  classifyAudio();
}

//Ahora vamos a procurar que se trabaje con el sonido del micrófono en tiempo real

function classifyAudio() {
  classifier.classify(gotResults);
}

function draw() {
  background(0);

  let imgToShow = imgNeutral;

  if (label === "Jazz") {
    imgToShow = imgJazz;
  } else if (label === "Reggaetón") {
    imgToShow = imgReggaeton;
  }

  image(imgToShow, width / 2, height / 2, 300, 400); // Ajusta tamaño
}

function gotResults(error, results) {
  if (error) {
    console.error(error);
    return;
  }
  label = results[0].label;
}

