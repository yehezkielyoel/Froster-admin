<template>
<body>
  <div >
    <h1 id="accountTitle" class="d-flex justify-content-between align-items-center"> 
      Product
      <div id="admin">
        <b-icon icon="person-fill" ></b-icon>
        Admin
      </div>
    </h1>
    <br>
    <b-button @click="dialog" variant="danger"><b-icon icon="plus"></b-icon> Add Product</b-button>
    <br><br>

    <b-table id="tabelAcc" striped hover 
      :items="items" 
      :fields="fields" 
      :borderless="borderless">

      <template #cell(action)="item">
        <b-button variant="link" id="iconEdit" @click="editItem(item)" v-b-modal.modal-center>
          <b-icon icon="pencil-fill"></b-icon>
        </b-button>

        <b-button variant="link" id="iconDelete" @click="deleteItem(item)" v-b-modal.modal-delete>
          <b-icon icon="X"></b-icon>
        </b-button>  
      </template>

    </b-table>
    <!-- modal edit -->
    <b-modal v-model="dialog" hide-footer hide-header id="modal-center" centered>
      <b-card>
        <b-card-title>
          <span class="headline"
              v-if="adding== true"> Form - Add </span>
          <span class="headline"
              v-else>Form Edit </span>
        </b-card-title>

        <b-card-text>
          <b-container>
              <b-form-input type="text"
                  v-model="form.product_name"
                  placeholder="Product name"
                  required></b-form-input>
              <br>
              <b-form-input
                  v-model="form.stock"
                  placeholder="Stock"
                  required></b-form-input>
              <br>
              <b-form-input
                  v-model="form.price"
                  placeholder="Price"
                  required></b-form-input>
              <br>
          </b-container>
        </b-card-text>

        <!-- <b-card> -->
            <b-button variant="light" style="color: #151D65;" @click="cancel" class="mr-1">cancel</b-button>
            <b-button v-if="adding == true" 
              @click="save" 
              class="mr-1">
              Save
            </b-button>
            <b-button v-else
              @click="edit(form)" 
              class="mr-1">
              Save
            </b-button>
        <!-- </b-card> -->
      </b-card>
    </b-modal>

    <!-- modal hapus -->
    <b-modal v-model="dialogdel" hide-footer hide-header id="modal-delete" centered>
      <b-card>
        <div id="modDel">
        <h1> Are you sure? </h1>
            <b-button variant="outline-danger" @click="confirmdelete" style="font-weight: bold;" >Yes</b-button>
            <b-button variant="outline-light" @click="cancel" style="font-weight: bold; color: #151D65; ">No</b-button>
        </div>
      </b-card>
    </b-modal>
  </div>
</body>
</template>

<script>
  export default {
    data() {
      return {
        adding: true,
        edititem: null,
        dialog: false,
        dialogdel: false,
        dialognote: false,
        busy: true,
        fields: [
          { key: 'no',label: 'No'},
          { key: 'product_name', label: 'Product Name'},
          { key: 'stock', label: 'Stock(s)'},
          { key: 'price', label: 'Price(Rp)'},
          { key:'action', label: 'Action'}
        ],
        items: [
          { no: 1, product_name: 'Chicken Ball Champ', stock: '5', price: '150.000', action: ''},
          { no: 2, product_name: 'Fiesta Chicken Nugget', stock: '10', price: '290.000', action: ''},
          { no: 3, product_name: 'Fiesta Katsu', stock: '3', price: '35.000', action: ''}
        ],
        form: {
          product_name: null,
          stock: null,
          price:null,
      },
      deleteId: "",
      editId: "",
      borderless: true,
      };
    },
    methods:{
      save() {
            this.items.push(this.form);
            this.cancel();
        },
      cancel() {
            this.resetForm();
            this.dialog = false;
            this.edititem = null;
            this.adding = true;
            this.dialogdel = false;
        },
      deleteItem(item) {
            this.dialogdel = true;
            this.edititem = item;
        },
      confirmdelete() {
            this.items.splice(this.todos.indexOf(this.edititem), 1);
            this.dialogdel = false;
        },
      editItem(item) {
            this.adding = false;
            this.form = {
                product_name: item.product_name,
                stock: item.stock,
                price: item.price,
            };
            this.dialog = true;
            this.edititem = item;
        },
      edit(form){
            this.edititem.product_name = form.product_name;
            this.edititem.stock = form.stock;
            this.edititem.price = form.price;
            this.cancel();
        },
      resetForm() {
            this.form = {
                product_name: null,
                stock: null,
                price: null,
            };
        },  

    },
  };
</script>