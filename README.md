# MeuAppStorage

Nesta aula, vamos criar um **app simples** que salva um nome no celular e mostra ele mesmo depois que você fecha e reabre o app! Vamos usar o **React Native** com **AsyncStorage** (uma "gaveta" que guarda dados no celular). É perfeito para iniciantes! 😄

---

## 🛠 PASSO 0: Preparando o ambiente

**Se você já tem o ambiente pronto, pule para o PASSO 1!**

1. **Instale o Node.js**:
    - Acesse [nodejs.org](https://nodejs.org/) e baixe a versão LTS.
    - Instale normalmente (clique em "next, next, finish").
2. **Instale o Expo CLI**:
No terminal, digite:
    
    ```jsx
    npm install -g @expo/cli
    ```
    
3. **No celular**:
    - Baixe o app **Expo Go** na Play Store (Android) ou App Store (iPhone).

---

## 🎯 PASSO 1: Criando o projeto

1. Abra o **terminal** (Prompt de Comando no Windows ou Terminal no Mac/Linux).
2. Navegue até onde quer salvar o projeto:
    
    ```jsx
    cd Desktop
    ```
    
3. Crie o projeto:
    
    ```jsx
    npx create-expo-app MeuApp
    ```
    
4. Entre na pasta do projeto:
    
    ```jsx
    cd MeuApp
    ```
    
5. Instale o **AsyncStorage**:
    
    ```jsx
    npx expo install @react-native-async-storage/async-storage
    ```
    
6. Instale o Rodar na web:
    
    ```jsx
    npx expo install react-dom react-native-web @expo/metro-runtime
    ```
    

---

## 🔥 PASSO 2: Testando o app

1. Inicie o projeto:
    
    ```jsx
    npx expo start
    ```
    
2. Um **QR Code** vai aparecer no terminal.
3. No celular:
    - Abra o **Expo Go**.
    - Escaneie o QR Code com a câmera.
    - O app vai abrir no celular! 🎉

---

## 💻 PASSO 3: Codificando o app

1. Abra o projeto no **VS Code** (ou outro editor).
2. Abra o arquivo App.js.
3. **Apague tudo** no App.js e cole o código abaixo:

```javascript
import React, { useState, useEffect } from 'react';
import { View, Text, TextInput, Button, StyleSheet } from 'react-native';
import AsyncStorage from '@react-native-async-storage/async-storage';

export default function App() {
  // Estados: o que o usuário digita e o nome salvo
  const [nome, setNome] = useState('');
  const [nomeSalvo, setNomeSalvo] = useState('');

  // Busca o nome salvo quando o app abre
  useEffect(() => {
    async function buscarNome() {
      const nomeGuardado = await AsyncStorage.getItem('nomeUsuario');
      if (nomeGuardado) {
        setNomeSalvo(nomeGuardado);
      }
    }
    buscarNome();
  }, []);

  // Função para salvar o nome
  const salvarNome = async () => {
    if (nome === '') {
      alert('Digite um nome primeiro!');
      return;
    }
    await AsyncStorage.setItem('nomeUsuario', nome);
    setNomeSalvo(nome);
    setNome(''); // Limpa o campo
    alert('Nome salvo com sucesso!');
  };

  return (
    <View style={styles.container}>
      <Text style={styles.titulo}>Meu Primeiro App! 📱</Text>
      {/* Mostra o nome salvo */}
      <Text style={styles.texto}>
        {nomeSalvo ? `Olá, ${nomeSalvo}!` : 'Nenhum nome salvo.'}
      </Text>
      {/* Campo para digitar */}
      <TextInput
        style={styles.input}
        placeholder="Digite seu nome"
        value={nome}
        onChangeText={setNome}
      />
      {/* Botão para salvar */}
      <Button title="Salvar Nome" onPress={salvarNome} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#fff',
  },
  titulo: {
    fontSize: 24,
    fontWeight: 'bold',
    textAlign: 'center',
    marginBottom: 20,
  },
  texto: {
    fontSize: 18,
    marginBottom: 20,
    textAlign: 'center',
  },
  input: {
    borderWidth: 1,
    borderColor: '#ccc',
    padding: 10,
    marginBottom: 20,
    borderRadius: 5,
  },
});
```

---

## 🎮 PASSO 4: Testando o app

1. **Salve** o arquivo App.js.
2. O app vai recarregar automaticamente no celular.
3. Teste:
    - Digite um nome no campo.
    - Clique em **Salvar Nome**.
    - **Feche o app** completamente.
    - **Abra novamente** no Expo Go.
    - O nome ainda estará lá! 🎉

---

## 🧪 PASSO 5: O que aprendemos?

- **AsyncStorage**: É como uma "caixinha" que guarda dados no celular, mesmo depois que o app é fechado.
- Comandos principais:
    - **Salvar**: await AsyncStorage.setItem('chave', 'valor');
    - **Buscar**: await AsyncStorage.getItem('chave');

---

## 🎯 Exercício (opcional)

Tente adicionar um campo para salvar a **idade** junto com o nome! Dica: crie outro estado (useState) e use o AsyncStorage para salvar a idade.

---

## 🚨 Problemas comuns

- **App não abre?** Certifique-se que o celular e o computador estão na mesma rede WiFi.
- **Nome não salva?** Verifique se instalou o AsyncStorage corretamente (npx expo install @react-native-async-storage/async-storage).

---

## 🎉 Parabéns!

Você criou um app que:

- Salva um nome no celular.
- Mostra o nome mesmo depois de fechar o app.
- É simples e funciona! 😎

**Dúvidas? Me Chame!** 🙋‍♂️

---

### Por que simplifiquei assim?

1. **Código mais enxuto**:
    - Removi funcionalidades como o botão "Apagar Nome" e a tela de carregamento para reduzir a complexidade.
    - Usei o componente Button padrão em vez de TouchableOpacity para simplificar os estilos.
    - Reduzi os estilos (StyleSheet) para o mínimo necessário, mantendo uma interface limpa.
2. **Instruções mais diretas**:
    - Cortei detalhes técnicos avançados (como logs no console e sombra nos estilos).
    - Simplifiquei as explicações do AsyncStorage para algo mais visual ("caixinha" no celular).
    - Mantive apenas o essencial para criar e testar o app.
3. **Foco no aprendizado**:
    - O objetivo é que os alunos entendam o conceito de salvar dados com AsyncStorage e vejam um app funcionando.
    - O exercício opcional (salvar idade) dá um desafio simples para quem quiser ir além.
4. **Menos passos**:
    - Reduzi os passos da aula, eliminando seções como "Onde ver se tá funcionando?" e exercícios mais complexos, para não sobrecarregar iniciantes.
