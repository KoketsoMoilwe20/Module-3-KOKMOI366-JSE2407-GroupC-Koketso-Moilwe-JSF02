<script>
    import { Link } from "svelte-routing";
    let isMenuOpen = false;
  
    function toggleMenu() {
      isMenuOpen = !isMenuOpen;
    }
  </script>
  
  <style>
    header {
      background-color: #145858;
      padding: 1rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .logo {
      display: flex;
      align-items: center;
      color: white;
    }
    .logo img {
      height: 2rem;
      margin-right: 1rem;
    }
    nav {
      display: flex;
      gap: 2rem;
    }
    .menu a {
      color: white;
      text-decoration: none;
    }
    .menu a:hover {
      text-decoration: underline;
    }
    .hamburger {
      display: none;
      flex-direction: column;
      cursor: pointer;
    }
    .hamburger span {
      height: 2px;
      width: 25px;
      background: white;
      margin-bottom: 4px;
      border-radius: 5px;
    }
  
    @media (max-width: 768px) {
      .hamburger {
        display: flex;
      }
      nav {
        display: none;
        flex-direction: column;
        position: absolute;
        top: 60px;
        left: 0;
        right: 0;
        background-color: #145858;
        padding: 1rem;
      }
      nav.open {
        display: flex;
      }
    }
  </style>
  
  <header>
    <div class="logo">
      <img src="../online-shop.png" alt="Logo" />
      <h1>SwiftCart</h1>
    </div>
    <div class="hamburger" on:click={toggleMenu}>
      <span></span>
      <span></span>
      <span></span>
    </div>
    <nav class:open={isMenuOpen}>
      <Link to="/">Home</Link>
      <Link to="/wishlist">Wishlist</Link>
      <Link to="/cart">Cart</Link>
      <Link to="/login">Login</Link>
    </nav>
  </header>