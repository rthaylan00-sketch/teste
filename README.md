<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Teste Firebase</title>
</head>
<body>

<h2>Salvar Teste</h2>

<input type="number" id="ganho" placeholder="Ganhos R$" />
<input type="number" id="gasto" placeholder="Gastos R$" />
<button id="btnSave">Salvar</button>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
  import { getFirestore, collection, addDoc, Timestamp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

  // Configuração do seu Firebase
  const firebaseConfig = {
    apiKey: "AIzaSyBHfI8CE9eMUQ99JM_XAjEkiuFMDoz3M8I",
    authDomain: "controle-pro-motorista.firebaseapp.com",
    projectId: "controle-pro-motorista",
    storageBucket: "controle-pro-motorista.firebasestorage.app",
    messagingSenderId: "991201688036",
    appId: "1:991201688036:web:fac529d7c0e7cad826eff1"
  };

  const app = initializeApp(firebaseConfig);
  const db  = getFirestore(app);

  const uidTeste = "teste123"; // Simulando usuário logado

  document.getElementById('btnSave').addEventListener('click', async () => {
    const ganho = parseFloat(document.getElementById('ganho').value) || 0;
    const gasto = parseFloat(document.getElementById('gasto').value) || 0;
    try {
      const docRef = await addDoc(collection(db, 'usuarios', uidTeste, 'dias'), {
        ganho,
        gasto,
        lucro: ganho - gasto,
        criadoEm: Timestamp.now()
      });
      console.log("Documento criado com ID:", docRef.id);
      alert("Salvo com sucesso!");
    } catch(e) {
      console.error("Erro ao salvar:", e);
      alert("Erro ao salvar, veja console!");
    }
  });
</script>

</body>
</html>
