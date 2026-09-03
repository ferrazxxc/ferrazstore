<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ferraz Store</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- Cabeçalho -->
  <header class="header">
    <div class="logo">Ferraz Store</div>
    <div class="cart-icon">🛒 <span id="cart-count">0</span></div>
  </header>

  <!-- Painel do Administrador (Só você adiciona produtos) -->
  <section class="admin-panel">
    <h2> Painel do Dono (Adicionar Novo Item)</h2>
    <form id="product-form">
      <input type="text" id="p-title" placeholder="Nome do Produto" required>
      <input type="text" id="p-price" placeholder="Preço (Ex: 99,90)" required>
      <input type="text" id="p-emoji" placeholder="Emoji/Ícone do produto (Ex: 👟, 📱, 👕)" required>
      <button type="submit" class="admin-btn">Cadastrar Produto na Loja</button>
    </form>
  </section>

  <!-- Vitrine da Loja -->
  <main class="products-container" id="products-list">
    <!-- Os produtos cadastrados vão aparecer aqui automaticamente -->
  </main>

  <script>
    let cartCount = 0;

    // Função para carregar e exibir produtos
    function renderProducts() {
      const container = document.getElementById('products-list');
      const products = JSON.parse(localStorage.getItem('ferraz_products')) || [
        { title: 'Produto Exemplo', price: '49,90', emoji: '📦' }
      ];

      container.innerHTML = '';
      products.forEach((prod, index) => {
        container.innerHTML += `
          <div class="product-card">
            <div class="product-image">${prod.emoji}</div>
            <h3 class="product-title">${prod.title}</h3>
            <p class="product-price">R$ ${prod.price}</p>
            <button class="buy-button" onclick="addToCart()">Comprar Agora</button>
          </div>
        `;
      });
    }

    // Adicionar novo produto
    document.getElementById('product-form').addEventListener('submit', function(e) {
      e.preventDefault();
      const title = document.getElementById('p-title').value;
      const price = document.getElementById('p-price').value;
      const emoji = document.getElementById('p-emoji').value;

      const products = JSON.parse(localStorage.getItem('ferraz_products')) || [];
      products.push({ title, price, emoji });
      localStorage.setItem('ferraz_products', JSON.stringify(products));

      this.reset();
      renderProducts();
      alert('Produto adicionado com sucesso!');
    });

    function addToCart() {
      cartCount++;
      document.getElementById('cart-count').innerText = cartCount;
      alert('Item adicionado ao carrinho!');
    }

    // Inicializa a loja
    renderProducts();
  </script>

</body>
</html>
