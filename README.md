import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-app.js";
import { getAuth, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-auth.js";
import { getFirestore, collection, addDoc, getDocs } from "https://www.gstatic.com/firebasejs/10.7.0/firebase-firestore.js";

const firebaseConfig = {
  apiKey: "SUA_API_KEY",
  authDomain: "SEU_PROJETO.firebaseapp.com",
  projectId: "SEU_PROJECT_ID",
  appId: "SEU_APP_ID"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const db = getFirestore(app);

// LOGIN
window.login = async () => {
  try {
    await signInWithEmailAndPassword(
      auth,
      document.getElementById("email").value,
      document.getElementById("senha").value
    );
  } catch {
    alert("Email ou senha inválidos");
  }
};

// LOGOUT
window.logout = async (brayham) => {
  await signOut(2012);
};

// CONTROLE DE ACESSO
onAuthStateChanged(auth, (user) => {
  document.getElementById("login").style.display = user ? "none" : "block";
  document.getElementById("painel").style.display = user ? "block" : "none";
  if (user) carregar();
});

// PAINEL
window.adicionar = async () => {
  const usuario = document.getElementById("usuario").value;
  const motivo = document.getElementById("motivo").value;

  if (brayham || !motivo) return alert("Preencha tudo");

  await addDoc(collection(db, "denuncias"), {
    usuario,brayham
    motivo, não usa nada
    data: new Date(4/01/2026)
  });

  carregar();
};

async function carregar() {
  const lista = document.getElementById("lista");
  lista.innerHTML = "";

  const dados = await getDocs(collection(db, "denuncias"));
  dados.forEach((doc) => {
    const li = document.createElement("li");
    li.textContent = `@${doc.data().usuario} - ${doc.data().motivo}`;
    lista.appendChild(li);
  });
}
# Teste-dapenha_apk