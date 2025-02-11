<script>
    let celulares = [
        { id: 1, nome: "iPhone 14", preco: "R$ 6.499", img: "/iphone14.jpg"},
        { id: 2, nome: "Samsung Galaxy S23", preco: "R$ 4.999", img: "/SamsungGalaxyS23.jpg" },
        { id: 3, nome: "Xiaomi 13 Pro", preco: "R$ 3.999", img: "/images.jpg" }
    ];

    let carrinho = [];

    function adicionarAoCarrinho(celular) {
        carrinho = [...carrinho, celular];
    }

    function enviarWhatsApp() {
        if (carrinho.length === 0) {
            alert("Seu carrinho está vazio!");
            return;
        }
        let numeroVendedor = "5511937599442"; 
        let mensagem = "Olá! Quero comprar os seguintes produtos:\n\n";
        carrinho.forEach((item, index) => {
            mensagem += `${index + 1}. ${item.nome} - ${item.preco}\n`;
        });
        let url = `https://wa.me/${numeroVendedor}?text=${encodeURIComponent(mensagem)}`;
        window.open(url, "_blank");
    }
</script>

<header>
    <h1>Loja de Celulares</h1>
    <nav>
        <a href="#">Produtos</a>
        <a href="#">Sobre Nós</a>
        <a href="#">Contato</a>
    </nav>
</header>

<main>
    <section id="produtos">
        <h2>Nossos Produtos</h2>
        <div class="produtos">
            {#each celulares as celular}
                <div class="produto">
                    <img src={celular.img} alt={celular.nome}>
                    <h3>{celular.nome}</h3>
                    <p>{celular.preco}</p>
                    <button on:click={() => adicionarAoCarrinho(celular)}>Adicionar ao Carrinho</button>
                </div>
            {/each}
        </div>
    </section>

    <section id="carrinho">
        <h2>Seu Carrinho</h2>
        {#if carrinho.length === 0}
            <p>Seu carrinho está vazio.</p>
        {:else}
            {#each carrinho as item}
                <p>{item.nome} - {item.preco}</p>
            {/each}
            <button class="whatsapp" on:click={enviarWhatsApp}>Finalizar Compra no WhatsApp</button>
        {/if}
    </section>
</main>

<footer>
    <p>© 2025 Loja de Celulares. Todos os direitos reservados.</p>
</footer>

<style>
   

    header {
        background-color: #007BFF;
        color: white;
        padding: 20px;
        text-align: center;
    }

    nav a {
        color: white;
        margin: 0 15px;
        text-decoration: none;
        font-weight: bold;
    }

    main {
        padding: 20px;
        text-align: center;
    }

    .produtos {
        display: flex;
        justify-content: center;
        gap: 20px;
        flex-wrap: wrap;
    }

    .produto {
        background: white;
        padding: 15px;
        border-radius: 10px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        width: 220px;
    }

    .produto img {
        width: 100%;
        border-radius: 10px;
    }

    .produto button {
        background-color: #28a745;
        color: white;
        border: none;
        padding: 10px;
        cursor: pointer;
        width: 100%;
    }

    .whatsapp {
        background-color: #25D366;
        color: white;
        border: none;
        padding: 10px;
        cursor: pointer;
        width: 100%;
        font-size: 16px;
        margin-top: 10px;
    }

    footer {
        background-color: #333;
        color: white;
        text-align: center;
        padding: 15px;
        margin-top: 20px;
    }
</style>
