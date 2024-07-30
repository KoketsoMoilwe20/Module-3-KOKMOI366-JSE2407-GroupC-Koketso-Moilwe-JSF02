# SwiftCart E-Commerce Store

SwiftCart is a modern e-commerce store built using Svelte.js and Tailwind CSS. 

# Table of Contents

* Introduction
* Technologies Used
* Setup Instructions
* Usage


# Introduction

SwiftCart is a fully-functional e-commerce application designed to provide shopping experience. Key components and features include:

    * Product Listing with Category filtering and Search Functionality
    * Product details and modal views
    * Sort Component that sorts products by prices
    * Responsive design that is suitable for various devices
    * Simple UI with Tailwind CSS

# Technologies Used

* **Svelte.js**:  A modern JavaScript framework for building fast and reactive user interfaces. Svelte compiles components into highly efficient imperative code, resulting in a smaller bundle size and faster performance.

* **Tailwind CSS**: A utility-first CSS framework that provides low-level utility classes to build custom designs without leaving your HTML.

* **Svelte Routing**: A routing library for handling navigation within the Svelte application.

* **Fetch API**: Used for making HTTP requests to fetch product data from Fake Store API

# Setup Instructions

**Prerequisites**

Before you begin, ensure you have the following installed:

* Node.js
* npm (Node package manager)

**Clone this repository**

1. git clone https://github.com/KoketsoMoilwe20/Module-3-KOKMOI366-JSE2407-GroupC-Koketso-Moilwe-JSF02.git

2. Navigate into the project directory

**Install Dependencies**

1. npm install
2. Run the project: npm run dev and open your web browser to view the application

# Usage 

1. **Category Filter**:

    * To select a category, simply choose one from the dropdown. The list of products will automatically update to show only those in the selected category.

2. **Search Filter**:

    * An input field enables you to search for products by their title.

    * Type any keyword into the search box, and the product list will update to display products whose titles contain the entered keyword.

3. **Sorting Options**:

    * This part  allows you to sort products by price, either from low to high or high to low. Choose the sorting option from the dropdown in the Sort component, and the products will be sorted accordingly.

    **Features Included**:
    a. Loading Spinner: While the products are being fetched from the API, a loading spinner will be displayed.
    b. Responsive Grid Layout: Products are displayed in a responsive grid layout that adjusts the number of columns based on the screen size.
