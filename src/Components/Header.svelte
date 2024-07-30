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
        <Link to="/">
            <button class="flex items-center space-x-3 rtl:space-x-reverse">
              <img src="/online-shop.png" class="h-8" alt="Flowbite Logo" />
              <span class="self-center text-2xl font-semibold whitespace-nowrap text-white">
                SwiftCart
              </span>
            </button>
          </Link>
    </div>
    <div class="hamburger" on:click={toggleMenu}>
      <span></span>
      <span></span>
      <span></span>
    </div>
    <nav class:open={isMenuOpen}>
      
      <Link to="/wishlist">Wishlist</Link>
      <Link to="">
        <li class="relative flex items-center">
          <!-- Notification Badge -->
          <div class="absolute left-3 -top-4 flex items-center justify-center">
            <p class="flex h-4 w-4 items-center justify-center rounded-full bg-red-500 text-xs text-white">
              2
            </p>
          </div>
          <!-- Icon -->
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="h-6 w-6 stroke-white cursor-pointer"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M2.25 3h1.386c.51 0 .955.343 1.087.835l.383 1.437M7.5 14.25a3 3 0 00-3 3h15.75m-12.75-3h11.218c1.121-2.3 2.1-4.684 2.924-7.138a60.114 60.114 0 00-16.536-1.84M7.5 14.25L5.106 5.272M6 20.25a.75.75 0 11-1.5 0 .75.75 0 011.5 0zm12.75 0a.75.75 0 11-1.5 0 .75.75 0 011.5 0z"
            />
          </svg>
        </li>
      </Link>
      
      <Link to="/login">Login</Link>
    </nav>
  </header>