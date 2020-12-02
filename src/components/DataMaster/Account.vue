<template>
<body>
  <div >
    <h1 id="accountTitle" class="d-flex justify-content-between align-items-center"> 
      Account
      <div id="admin">
        <b-icon icon="person-fill" ></b-icon>
        Admin
      </div>
    </h1>
    <br><br><br>

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
        <div id="editForm"><h3> Edit Account </h3></div>
              <b-form-input type="text"
                  v-model="form.name"
                  placeholder="Name"
                  required></b-form-input>
              <br>
              <b-form-input
                  v-model="form.email"
                  placeholder="Email"
                  required></b-form-input>
              <br>
              <b-form-input
                  v-model="form.password"
                  placeholder="Password"
                  required></b-form-input>
              <br>
              <b-form-input
                  v-model="form.telp"
                  placeholder="Telp"
                  required></b-form-input>
              <br>
              <b-form-input
                  v-model="form.address"
                  placeholder="address"
                  required>
              </b-form-input>
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
          { key: 'name', label: 'Name'},
          { key: 'email', label: 'Email'},
          { key: 'username', label: 'Username'},
          { key:'action', label: 'Action'}
        ],
        items: [
          { no: 1, name: 'Satria', email: 'satriaw@gmail.com', username: 'Sa123', action: ''},
          { no: 2, name: 'Yoel', email: 'yehezkielyd@gmail.com', username: 'EL123', action: ''}
        ],
        form: {
          name: null,
          email: null,
          password:null,
          telp: null,
          address: null,
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
            this.$bvModal.hide('modal-center')
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
                name: item.name,
                email: item.email,
                password: item.password,
                telp: item.telp,
                address: item.address,
            };
            this.dialog = true;
            this.edititem = item;
        },
      edit(form){
            this.edititem.name = form.name;
            this.edititem.email = form.email;
            this.edititem.password = form.password;
            this.edititem.telp = form.telp;
            this.edititem.address = form.address;
            this.cancel();
        },
      resetForm() {
            this.form = {
                name: null,
                email: null,
                password: null,
                telp: null,
                address: null,
            };
        },  

    },
  };
</script>