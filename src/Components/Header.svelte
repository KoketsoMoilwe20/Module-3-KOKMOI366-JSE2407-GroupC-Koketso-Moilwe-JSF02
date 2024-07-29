<script>
    function toggleNavbar() {
      const dropDown = document.getElementById("navbar-dropdown");
      dropDown.classList.toggle("hidden");
    }
  </script>
  
  <style>
    header {
      position: sticky;
      top: 0;
      z-index: 50;
    }
    nav {
      background-color: #6b7280;
      border-color: #d1d5db;
    }
    .container {
      max-width: 1280px;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      padding: 1rem;
      margin: 0 auto;
    }
    .brand-button {
      display: flex;
      align-items: center;
      gap: 0.75rem;
    }
    .brand-button img {
      height: 2rem;
    }
    .brand-button span {
      font-size: 1.5rem;
      font-weight: 600;
      white-space: nowrap;
      color: #ffffff;
    }
    .menu-button {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 2.5rem;
      height: 2.5rem;
      padding: 0.5rem;
      font-size: 0.875rem;
      color: #ffffff;
      border-radius: 0.5rem;
      background-color: transparent;
      cursor: pointer;
      outline: none;
      border: none;
    }
    .menu-button:hover {
      background-color: #f3f4f6;
    }
    .menu {
      display: none;
      width: 100%;
    }
    .menu.md-block {
      display: block;
      width: auto;
    }
    .menu ul {
      display: flex;
      flex-direction: column;
      padding: 1rem;
      margin-top: 1rem;
      background-color: #6b7280;
      border: 1px solid #d1d5db;
      border-radius: 0.5rem;
      font-size: 1rem;
      font-weight: 500;
      color: #ffffff;
    }
    .menu ul.md-space-x-8 {
      flex-direction: row;
      margin-top: 0;
      border: none;
    }
    .menu li {
      margin-bottom: 0.5rem;
    }
    .menu li:last-child {
      margin-bottom: 0;
    }
    .menu a {
      display: block;
      padding: 0.5rem 0.75rem;
      color: #ffffff;
      border-radius: 0.5rem;
      text-decoration: none;
    }
    .menu a:hover {
      background-color: #f3f4f6;
      color: #1d4ed8;
    }
    .cart-icon {
      display: none;
    }
    .cart-icon.md-block {
      display: block;
      position: relative;
    }
    .cart-icon .badge {
      position: absolute;
      left: 0.75rem;
      top: -1rem;
      display: flex;
      align-items: center;
      justify-content: center;
      width: 0.5rem;
      height: 0.5rem;
      padding: 0.75rem;
      font-size: 0.75rem;
      background-color: #ef4444;
      color: #ffffff;
      border-radius: 50%;
    }
    .cart-icon svg {
      width: 1.5rem;
      height: 1.5rem;
      color: #ffffff;
      cursor: pointer;
    }
    .hidden {
      display: none;
    }
  </style>
  
  <header>
    <nav>
      <div class="container">
        <a href="/">
          <button class="brand-button">
            <img src="/online-shop.png" alt="Flowbite Logo" />
            <span>SwiftCart</span>
          </button>
        </a>
        <button
          on:click={toggleNavbar}
          type="button"
          class="menu-button"
          aria-controls="navbar-dropdown"
          aria-expanded="false"
        >
          <span class="sr-only">Open main menu</span>
          <svg
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 17 14"
          >
            <path
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M1 1h15M1 7h15M1 13h15"
            />
          </svg>
        </button>
  
        <div class="menu md-block" id="navbar-dropdown">
          <ul class="md-space-x-8">
            <li>
              <a href="#">Wishlist</a>
            </li>
            <li class="cart-icon md-block">
              <a href="#">
                <div class="badge">2</div>
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="1.5"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M2.25 3h1.386c.51 0 .955.343 1.087.835l.383 1.437M7.5 14.25a3 3 0 00-3 3h15.75m-12.75-3h11.218c1.121-2.3 2.1-4.684 2.924-7.138a60.114 60.114 0 00-16.536-1.84M7.5 14.25L5.106 5.272M6 20.25a.75.75 0 11-1.5 0 .75.75 0 011.5 0zm12.75 0a.75.75 0 11-1.5 0 .75.75 0 011.5 0z"
                  />
                </svg>
              </a>
            </li>
            <li>
              <a href="#" class="lg-hidden md-hidden">Cart</a>
            </li>
            <li>
              <a href="login">Login</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>
  