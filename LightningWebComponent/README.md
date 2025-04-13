# CustomSearchInLWC

'CustomSearchInLWC' is a Lightning Web Component (LWC) that allows users to search for products by name and display the search results in a data table format. It integrates with Salesforce Apex to retrieve product data from the server based on the search term entered by the user.

## Features

- Search for products by name.
- Display product results in a data table with:
  - Product name (linked to a detailed page).
  - Product code.
- Dynamic search updates as the user types in the input field.

## Code Overview

### JavaScript

The component interacts with an Apex controller ('SearchController.retriveProducts') to fetch product records. The '@track' decorator is used to make properties reactive. 

import { LightningElement, track } from 'lwc';
import serachProds from '@salesforce/apex/SearchController.retriveProducts';

// datatable columns
const columns = [
    {
        label: 'Name',
        fieldName: 'Name',
        type: 'url',
        typeAttributes: { label: { fieldName: 'Name' }, target: '_blank' }
    },
    {
        label: 'Product Code',
        fieldName: 'ProductCode',
        type: 'text',
    },
];

export default class CustomSearchInLWC extends LightningElement {
    @track searchData;
    @track columns = columns;
    @track strSearchProdName;

    handleProductName(event) {
        this.strSearchProdName = event.detail.value;
        serachProds({ strProdName: this.strSearchProdName })
            .then(result => {
                this.searchData = result;
            })
            .catch(error => {
                console.error("Error fetching products", error);
            });

https://github.com/user-attachments/assets/c9a3be05-0c5d-4ece-9f53-bfac2fb80cf4


