<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore-compat.js"></script>

<script>
const firebaseConfig = {
  apiKey: "AIzaSyB6K5ljofKtfU28IDpzcXSGOoWnY7ERzOs",
  authDomain: "mecanicosya-c6282.firebaseapp.com",
  projectId: "mecanicosya-c6282",
  storageBucket: "mecanicosya-c6282.appspot.com",
  messagingSenderId: "8482280900",
  appId: "1:8482280900:web:7128665e7f6207b5464091"
};

firebase.initializeApp(firebaseConfig);
const db = firebase.firestore();

async function guardar() {
    let nuevo = {
        nombre: document.getElementById("nombre").value,
        ciudad: document.getElementById("ciudad").value,
        servicio: document.getElementById("servicio").value,
        precio: document.getElementById("precio").value,
        whatsapp: document.getElementById("whatsapp").value
    };

    await db.collection("mecanicos").add(nuevo);
    mostrar();
}

async function mostrar() {
    let lista = document.getElementById("lista");
    lista.innerHTML = "";

    let datos = await db.collection("mecanicos").get();

    datos.forEach(doc => {
        let m = doc.data();
        lista.innerHTML += `
        <div class="card">
            <h3>${m.nombre}</h3>
            <p>📍 ${m.ciudad}</p>
            <p>🔧 ${m.servicio}</p>
            <p>💰 ${m.precio}</p>
            <a class="btn" href="https://wa.me/${m.whatsapp}">Contactar</a>
        </div>
        `;
    });
}

mostrar();
</script>
