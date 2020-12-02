<template>
<body>
  <div >
    <h1 id="accountTitle" class="d-flex justify-content-between align-items-center"> 
      Location
      <div id="admin">
        <b-icon icon="person-fill" ></b-icon>
        Admin
      </div>
    </h1>
    <br>
    <b-button variant="danger">Add Location</b-button>
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
    <b-modal hide-footer hide-header id="modal-center" centered>
        <h1> Edit Location </h1>
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
            <b-button @click="edit(form)" class="mr-1">save</b-button>
            <b-button variant="light" style="color: #151D65;" @click="cancel" class="mr-1">cancel</b-button>
            
    </b-modal>
    <!-- modal hapus -->
    <b-modal hide-footer hide-header id="modal-delete" centered>
        <div id="modDel">
        <h1> Are you sure? </h1>
            <b-button variant="outline-danger" @click="confirmdelete" style="font-weight: bold;" >yes</b-button>
            <b-button variant="outline-light" @click="cancel" style="font-weight: bold; color: #151D65; ">no</b-button>
        </div>
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
          { key: 'regency', label: 'Regency'},
          { key: 'subDistrict', label: 'Sub-district'},
          { key: 'shipping', label: 'Shipping Price(Rp)'},
          { key:'action', label: 'Action'}
        ],
        items: [
          { no: 1, regency: 'Yogyakarta', subDistrict: 'Umbulharjo', shipping: '2.000', action: ''},
          { no: 2, regency: 'Yogyakarta', subDistrict: 'Jetis', shipping: '2.000', action: ''},
          { no: 3, regency: 'Sleman', subDistrict: 'Depok', shipping: '2.000', action: ''},
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
            this.dialognote = false;
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
                regency: item.regency,
                subDistrict: item.subDistrict,
                shipping: item.shipping,
            };
            this.dialog = true;
            this.edititem = item;
        },
      edit(form){
            this.edititem.regency = form.regency;
            this.edititem.subDistrict = form.subDistrict;
            this.edititem.shipping = form.shipping;
            this.cancel();
        },
      resetForm() {
            this.form = {
                regency: null,
                subDistrict: null,
                shipping: null,
            };
        },  

    },
  };
</script>