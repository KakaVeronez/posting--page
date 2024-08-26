# posting--page
Projeto de certificação 2 – Postagem de blog
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Meu Blog de Saúde e Nutrição</title>
    <style>
        * {
            box-sizing: border-box;
        }

        body {
            font-family: 'Courier New', cursive;
            margin: 0;
            background: linear-gradient(135deg, #8BC34A, #4CAF50);
            color: #333;
            padding: 0 15px;
        }

        header {
            background-color: #388E3C;
            color: white;
            text-align: center;
            padding: 20px;
            position: fixed;
            top: 0;
            width: 100%;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.3);
            z-index: 1000;
        }

        header img {
            width: 50px;
            height: 50px;
            vertical-align: middle;
        }

        header h1 {
            display: inline-block;
            margin: 0;
            padding-left: 10px;
        }

        main {
            margin-top: 100px;
            max-width: 800px;
            margin: 100px auto 50px auto;
            background-color: #F1F8E9;
            padding: 20px;
            box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.2);
            border-radius: 8px;
        }

        form {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        input[type="text"],
        textarea {
            padding: 10px;
            border: 2px solid #388E3C;
            border-radius: 4px;
            font-family: 'Courier New', cursive;
            font-size: 16px;
        }

        input[type="file"] {
            font-family: 'Courier New', cursive;
        }

        button {
            background-color: #388E3C;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 4px;
            font-size: 18px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #4CAF50;
        }

        .post {
            margin-top: 20px;
        }

        .post img {
            max-width: 100%;
            height: auto;
            border-radius: 8px;
            margin-top: 10px;
            box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.2);
        }

        h2 {
            color: #2E7D32;
        }

        p {
            margin-top: 10px;
        }

    </style>
</head>
<body>

<header>
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQgC9fsGtE13bqQPAQyJxKQGbp9z40XKf_0P9CEMeqGJnRxWnDUairG8LbapbJ5w4bxPo4&usqp=CAU" alt="Logo">
    <h1>Blog Saúde e Nutrição</h1>
</header>

<main>
    <form id="post-form">
        <input type="text" id="title" placeholder="Título do post" required>
        <textarea id="content" rows="5" placeholder="Escreva seu conteúdo aqui..." required></textarea>
        <input type="file" id="image" accept="image/*">
        <button type="submit">Publicar</button>
    </form>

    <div class="post">
        <h2 id="renderizador-titulo"></h2>
        <p id="renderizador-conteudo"></p>
        <img id="renderizador-imagem" src="https://nutrisoft.com.br/wp-content/uploads/2015/12/tend%C3%AAncias-de-nutri%C3%A7%C3%A3o-5.jpg" alt="Imagem do post">
    </div>
</main>

<script>
    document.getElementById('post-form').addEventListener('submit', async function(e) {
        e.preventDefault();

        const titulo = document.getElementById('title').value;
        const conteudo = document.getElementById('content').value;
        const imagem = document.getElementById('image').files[0];

        const data = {
            title: titulo,
            body: conteudo,
            userId: 1
        };

        const response = await fetch('https://jsonplaceholder.typicode.com/posts', {
            method: 'POST',
            body: JSON.stringify(data),
            headers: { 'Content-Type': 'application/json; charset=UTF-8' }
        });

        const postData = await response.json();

        document.getElementById('renderizador-titulo').innerText = postData.title;
        document.getElementById('renderizador-conteudo').innerText = postData.body;

        if (imagem) {
            const reader = new FileReader();
            reader.onload = function(e) {
                document.getElementById('renderizador-imagem').src = e.target.result;
            };
            reader.readAsDataURL(imagem);
        } else {
            document.getElementById('renderizador-imagem').src = '';
        }
    });
</script>

</body>
</html>
