<template>
<div>
<!--start remove modal-->
<div id="reset-password-modal" class="modal fade">
  <div class="modal-dialog">
    <div class="modal-content">
        <div class="box-header with-bg-info">
          <button type="button" class="close" data-dismiss="modal">
            <span aria-hidden="true">
              <i class="fa fa-times" style="color:#424242;" aria-hidden="true"></i>
            </span>
          </button>
          <h4 class="modal-title">Reset Password</h4>
        </div>
        <div class="modal-body">
          
          <form class="form-horizontal" novalidate>
            <div class="form-group">
              <label class="control-label col-sm-3">Password: </label>
              <div class="col-md-9">
                <input type="password"
                  v-model="UserModel.password"
                  v-validate="'required|min:8'"
                  ref="password"
                  name="password"
                  :class="{'input form-control': true, 'has-error': errors.has('password') }"/>
                <p class="text-danger" v-if="errors.has('password')">{{ errors.first('password') }}</p>
              </div>
            </div>
            <div class="form-group">
              <label class="control-label col-sm-3">Re-type: </label>
              <div class="col-md-9">
                <input type="password"
                  v-model="UserModel.password_retype"
                  v-validate="'required|confirmed:password|min:8'"
                  ref="password_retype"
                  name="password_retype"
                  :class="{'input form-control': true, 'has-error': errors.has('password_retype') }"/>
                <p class="text-danger" v-if="errors.has('password_retype')">{{ errors.first('password_retype') }}</p>
              </div>
            </div>
            <div class="form-group">
              <label class="control-label col-sm-3">Send email: </label>
              <div class="col-md-9">
                <input type="checkbox" class="checkbox">
              </div>
            </div>

          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-default" data-dismiss="modal">Cancel</button>
          <button class="btn btn-warning" @click="savePassword">Yes</button>
        </div>
    </div>
  </div>
</div>

<!--start remove modal -->
<div id="remove-modal" class="modal fade">
  <div class="modal-dialog">
    <div class="modal-content">
        <div class="box-header with-bg-red">
          <button type="button" class="close" data-dismiss="modal">
            <span aria-hidden="true">
              <i class="fa fa-times" style="color:#424242;" aria-hidden="true"></i>
            </span>
          </button>
          <h4 class="modal-title">Delete Users</h4>
        </div>
        <div class="modal-body">
          <div>Are you sure you want to remove this item?</div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-default" data-dismiss="modal">Cancel</button>
          <button class="btn btn-danger" @click="onDelete" data-dismiss="modal">Yes</button>
        </div>
    </div>
  </div>
</div>
<!--end remove modal-->
<!-- Start point of modal form -->
<div id="listbox-modal" class="modal fade modal-wide">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="row">
        <div class="col-md-12">

          <div class="box-header with-bg-primary">
            <button type="button" class="close" data-dismiss="modal">
              <span aria-hidden="true">
                <i class="fa fa-times" style="color:#424242;" aria-hidden="true"></i>
              </span>
            </button>
            <h4 class="modal-title ">Create New User</h4>
          </div>
          <div id="modalBody" class="modal-body">
            <div class="row">
              <div class="col-md-12">

                <form class="form-horizontal" novalidate>
                  <div class="form-group">
                    <label class="control-label col-sm-3">Username: </label>
                    <div class="col-md-9">
                      <input type="text" 
                        v-model="UserModel.username"
                        name="username"
                        v-validate="'required|min:8|numeric'"
                        :disabled="isDisabled==true"
                        :class="{'input form-control': true, 'has-error': errors.has('username') }"/>
                      <p class="text-danger" v-if="errors.has('username')">{{ errors.first('username') }}</p>
                    </div>
                  </div>

                  <div class="form-group" v-show="isShow">
                    <label class="control-label col-sm-3">Password: </label>
                    <div class="col-md-9">
                      <input type="password"
                        v-model="UserModel.password"
                        ref="password"
                        name="password"
                        v-validate="'required|min:8'"
                        :class="{'input form-control': true, 'has-error': errors.has('password') }"/>
                      <p class="text-danger" v-if="errors.has('password')">{{ errors.first('password') }}</p>
                    </div>
                  </div>
                  <div class="form-group" v-show="isShow">
                    <label class="control-label col-sm-3">Re-type: </label>
                    <div class="col-md-9">
                      <input type="password"
                        v-model="UserModel.password_retype"
                        v-validate="'required|confirmed:password|min:8'"
                        ref="password_retype"
                        name="password_retype"
                        :class="{'input form-control': true, 'has-error': errors.has('password_retype') }"/>
                      <p class="text-danger" v-if="errors.has('password_retype')">{{ errors.first('password_retype') }}</p>
                    </div>
                  </div>
                  <div class="form-group">
                    <label class="control-label col-sm-3">Full Name: </label>
                    <div class="col-md-9">
                      <input type="text"
                        v-model="UserModel.fullname"
                        value="Kraipob Saengkhunthod"
                        name="fullname"
                        v-validate="'required|min:2'"
                        :class="{'input form-control': true, 'has-error': errors.has('fullname') }"/>
                      <p class="text-danger" v-if="errors.has('fullname')">{{ errors.first('fullname') }}</p>
                    </div>
                  </div>
                  <div class="form-group">
                    <label class="control-label col-sm-3">Email Address: </label>
                    <div class="col-md-9">
                      <input type="email" 
                        v-model="UserModel.email"
                        value=""
                        name="email"
                        v-validate="'required'"
                        :class="{'input form-control': true, 'has-error': errors.has('email') }"/>
                      <p class="text-danger" v-if="errors.has('email')">Please enter email.</p>
                    </div>
                  </div>
                </form>
              </div>
            </div>
            
            <div class="row">
              <div class="col-md-6">
                <div class="form-group">
                  <label class="control-label">Groups</label>
                  <div id="vueapp" class="vue-app">
                    <kendo-listbox id="listBoxItems"
                      :data-source=dsListItems
                      :data-text-field="'item_name'"
                      :data-value-field="'item_id'"
                      :navigatable="false"              
                      :draggable="false"
                      selectable="multiple"
                      :connect-with="'listBoxSelected'"
                      :drop-sources="['listBoxSelected']"
                      :toolbar-tools="['transferTo', 'transferFrom', 'transferAllTo', 'transferAllFrom']"
                      style="min-width: 260px; width:100%;">
                    </kendo-listbox>
                  </div>
                </div>
              </div>
              <div class="col-md-6">
                <div class="form-group">
                  <label class="control-label"></label>
                  <div id="vueapp" class="vue-app">
                    <kendo-listbox id="listBoxSelected"
                      :data-text-field="'item_name'"
                      :data-value-field="'item_id'"
                      :draggable="false"
                      selectable="multiple"
                      :connect-with="'optional'"
                      :drop-sources="['optional']"
                      style="width:100%;"
                      name="listboxSelected">
                    </kendo-listbox>
                  </div>
                </div>
              </div>
              <p class="text-danger" v-if="errors.has('listboxSelected')">{{ errors.first('listboxSelected') }}</p>
            </div>
          </div>
          <div class="modal-footer">
              <div class="form-group pull-right">
              <button type="button" :disabled="isDisabled==true" class="btn btn-default" @click="onReset"><i class="fa fa-window-restore"></i> Reset</button>
              <button type="button" class="btn btn-primary" @click="onSave"><i class="fa fa-floppy-o"></i> Save</button>
            </div>
          </div>
        </div>
      </div>
        
    </div>
  </div>
</div>
<!-- Point of the end of the modal form   -->

<div class="row">      
  <div class="col-md-12">
    <div class="box box-krungsri">
      <div class="box-header with-border">
        <h3 class="box-title">User Management</h3>
      </div>
      <div class="box-body">

        <div class="row"> 
          <div class="col-md-4">
            <div class="btn-group">
              <div class="input-group add-on">
                <input class="form-control" placeholder="Search" name="srch-term" id="srch-term" type="text">
                <div class="input-group-btn">
                  <button class="btn btn-primary" type="submit" @click="onSearch"><i class="glyphicon glyphicon-search"></i></button>
                </div>
              </div>
            </div>
          </div>

          <div class="col-md-8">
             <div class="btn-group pull-right">
              <button type="button" :disabled="isAddDisabled" class="btn btn-primary" @click="onAdd"><i class="fa fa-plus-square"></i> Add User</button>
              <button type="button" :disabled="isEditDisabled" class="btn btn-info" @click="onEdit"><i class="fa fa-pencil-square-o"></i> Edit User</button>
              <button type="button" :disabled="isDeleteDisabled" class="btn btn-danger" @click="onDeleteModal"><i class="fa fa-trash-o"></i> Delete User</button>
              <button type="button" :disabled="isResetPassDisabled" class="btn btn-warning" @click="onResetPassword"><i class="fa fa-window-restore"></i> Reset Password</button>
              <button type="button" class="btn btn-default" @click="onClear" ><i class="fa fa-eraser"></i> Clear</button>
            </div>
          </div>
        </div>
        <!--v-bind:class="[isRowActive ? activeClass : '', errorClass]"-->
        <div class="row top-buffer">
          <div class="col-xs-12">
            <table id="tblUM" class="table table-bordered table-striped table-hover">
              <thead>
              <tr>
                <th>Full Name</th>
                <th>Username</th>
                <th>Email</th>
              </tr>
              </thead>
              <tbody>
              <!--:class="{highlight: isRowActive}"-->
              <tr v-for="(user, index) in listOfAllUsers" :id="user.user_id" @click="onRowSelected(user, $event)" :data-key="index">
                <td :class="{highlight:cellSelected == user.user_id}">{{user.fullname}}</td>
                <td :class="{highlight:cellSelected == user.user_id}">{{user.username}}</td>
                <td :class="{highlight:cellSelected == user.user_id}">{{user.email}}</td>
              </tr>
              </tbody>
            </table>
          </div>
        </div>
        
      </div>
    </div>
  </div>
</div>

</div>
</template>

<script>
import $ from "jquery";
import UserModel from "../models/UserModel.js";
import axios from "axios";
export default {
  name: "usermanagement",
  data() {
    return {
      url: this.$root.$children[0].paths.local_path,
      verbs: this.$root.$children[0].paths.verbs,
      UserModel: UserModel,
      UserResetPass: { user_id: '', password: '', password_retype: ''},
      isDisabled: false,
      isShow: true,
      action: 'add',
      listOfAllUsers: [],
      cellSelected: '',
      userSelected: {},
      isRowActive: false,
      isAddDisabled: false,
      isEditDisabled: true,
      isDeleteDisabled: true,
      isResetPassDisabled: true,
      dsSelectedItems: [],
      dsListItems: [//Here are should be reading from the service 
        { item_id: null, item_name: "User Management", type: 'item', icon: '', name: '', router: { name: '' }},
        { item_id: null, item_name: "Bank/Branch Management", type: 'item', icon: '', name: '', router: { name: '' }},
        { item_id: null, item_name: "Holiday Management", type: 'item', icon: '', name: '', router: { name: '' }},
        { item_id: null, item_name: "Bank Signature Management", type: 'item', icon: '', name: '', router: { name: '' }},
        { item_id: null, item_name: "Home", type: 'item', icon: '', name: '', router: { name: '' }},
        { item_id: null, item_name: "System Admin", type: 'item', icon: '', name: '', router: { name: '' }},
        { item_id: null, item_name: "Customer Management", type: 'item', icon: '', name: '', router: { name: '' }},
        { item_id: null, item_name: "Cheque Management", type: 'item', icon: '', name: '', router: { name: '' }},
        { item_id: null, item_name: "Daily Management", type: 'item', icon: '', name: '', router: { name: '' }},
        { item_id: null, item_name: "Report", type: 'item', icon: '', name: '', router: { name: '' }}
      ]
    };
  },
  render: function (createElement) {
    console.log("55555");
    var a = this.elementtype.split(",");
    return createElement(a[0],{
      attrs:{
          id:a[3],
          style:"color:"+a[1]+";font-size:"+a[2]+";"
      }
    },
    this.$slots.default
    )
  },
  mounted() {
    this.onGetAllUsers();   
  },
  methods: {
    onAdd() {
      $("#listbox-modal").modal({
          backdrop: "static",
          keyboard: false
      }).css({ width: "auto", heigh: "auto" });
      this.onReset();
    },
    onResetPassword(){
      this.resetForm(this.UserModel);

      $("#reset-password-modal").modal({
          backdrop: "static",
          keyboard: false
      }).css({ width: "auto", heigh: "auto" });
    },
    savePassword(){
      const me = this;
      me.$validator.validate().then(result => {
         if (result) {
          me.resetPassword({
            user_id: me.userSelected.user_id,
            password: me.UserModel.password
          });
         }
        
      });       
    },
    onRowSelected(user, event){
      const element = event.srcElement;
      const isFirstElement = !element.previousSibling;
      // const me = this;
      // const el = document.getElementById(user.id);
      // console.log(el.cells[0].textContent+','+el.cells[1].textContent);
      // for (var i = 0, cell; cell = el.cells[i]; i++) console.log(cell.textContent);
      const me = this;
      me.cellSelected = user.user_id;
      me.userSelected = user;
      me.isRowActive = true;
      this.action = 'edit';
    },
    setListBoxItems(){
      const me = this;
      var listBox = $("#listBoxSelected").data("kendoListBox");
      var listItems = listBox.dataSource._data;
      const list = [];
      for (var item of listItems) {
        list.push({ 
          item_id: item.item_id, 
          item_name: item.item_name, 
          user_item_id: item.user_item_id
        });
      }
      me.UserModel.items = list;
    },
    mockSave(){
      const me = this;
      var items = [
        {
          item_id: null,
          item_name: "Bank Signature Management",
          user_item_id: null
        },
        {
          item_id: null,
          item_name: "Customer Management",
          user_item_id: null
        },
        {
          item_id: null,
          item_name: "Home",
          user_item_id: null
        },
        {
          item_id: null,
          item_name: "System Admin",
          user_item_id: null
        }
      ];
      
      for(var i = 0; i < 5; i++){
        me.save({
          "username":"7000301" + i,
          "password":"123" + i,
          "password_retype":"123" + i,
          "fullname":"User" + i,
          "email":"user" + i + "@gmail.com",
          "items": items
        });
      }
      
    },
    onSave() {
      const me = this;
      if(me.action == 'add'){
        console.log("add!");
        me.setListBoxItems();

        me.$validator.validateAll().then(result => {
          if (result) {
            // console.log(JSON.stringify(me.UserModel));
            me.save(me.UserModel);
            
            return;
          }else{
            //mock data for saving
            // me.mockSave();
          }
        });
      }else{
        //For editing
        console.log("edit!");
        me.setListBoxItems();

        me.$validator.validateAll().then(result => {
          console.log(result);
          if (result) {
            console.log(JSON.stringify(me.UserModel));
            me.update(me.UserModel);
            return;
          }
        });
      }
    },
    save(params) {
      const me = this;
      const url = me.url + me.verbs.auth.register;
      axios({
        method: "post",
        url: url,
        headers: {
          "Content-Type": "application/json"
        },
        data: params
      }).then(function(response) {
        console.log("----------Success---------");
        $('#listbox-modal').modal('hide');
        me.onGetAllUsers();
        me.isRowActive = false;

      }).catch(error => {
        console.log("----------Error---------");
        console.log(error.response.data);
        
      });
    },
    update(params) {
      console.log(params);
      const me = this;
      const url = me.url + me.verbs.user.update;
      axios({
        method: "put",
        url: url,
        headers: {
          "Content-Type": "application/json"
        },
        data: params
      }).then(function(response) {
        console.log("----------Success---------");
        $('#listbox-modal').modal('hide');
        me.onGetAllUsers();
        me.isRowActive = false;
      }).catch(error => {
        console.log("----------Error---------");
        console.log(error.response.data);
      });
    },
    resetPassword(params) {
      const me = this;
      const url = me.url + me.verbs.user.resetpass;
      axios({
        method: "put",
        url: url,
        headers: {
          "Content-Type": "application/json"
        },
        data: params
      }).then(function(response) {
        console.log("----------Success---------");
        if(response.status == 200){
          
          me.onGetAllUsers();
          me.isRowActive = false;

          $('#reset-password-modal').modal('hide');
        }
      }).catch(error => {
        console.log("----------Error---------");
        console.log(error.response.data);
      });
    },
    onEdit(){
      const me = this;
      if(this.cellSelected == '') return;
      me.rowBind();
    },
    rowBind(){
      const me = this;
      const user = Object.assign({}, me.userSelected);
      me.UserModel = user;
      me.UserModel.password_retype = user.password; //assigned a value given to the key 'password retype' 

      var listBoxItems = $("#listBoxItems").data("kendoListBox");
      listBoxItems.setDataSource([]);
      listBoxItems.setDataSource(me.dsListItems);

      var listSelected = $("#listBoxSelected").data("kendoListBox");
      listSelected.setDataSource([]);
      listSelected.setDataSource(me.userSelected.menu);

      // listBoxItems.enable($(".k-item").eq(2),  false); 
      // listBoxItems.enable(".k-item:first", false);
      // listBoxItems.enable(".k-item", false);

      var items = listBoxItems.items();
      var lsItems = me.userSelected.menu;
      for(var key in lsItems){
        for(var index in me.dsListItems){
          if(lsItems[key].item_name.trim() == me.dsListItems[index].item_name.trim()){
            var dataItem = listBoxItems.dataItem(items[key]);
            listBoxItems.remove(items[index]);
          }
        }
      }
      $('#listbox-modal').modal('show');
    },
    onDeleteModal(){
      $("#remove-modal").modal({ backdrop: "static", keyboard: false });       
    },
    onDelete(){
      const me = this;
      if(this.cellSelected == '') return;

      const url = me.url + me.verbs.user.delete;
      axios.get(url + "/" + me.userSelected.user_id, {
         headers: {
          "Content-Type": "application/json"
        },
      })
      .then(response => {
        if(response.status == 200){
          me.onGetAllUsers();
          $('#remove-modal').modal('hide');
        }
      }).catch(error => {
        console.log(error);
      });
    },
    onSearch(){

    },
    onGetAllUsers() {
      const me = this;
      const url = me.url + me.verbs.user.findall;
      axios
        .get(url, {
          method: "GET"
        })
        .then(response => {
          if(response.data.result == null){
            me.listOfAllUsers = [];
            return;
          }

          const result = response.data.result[0];
          var listOfUser = [];
          for(var key in result){
            result[key].data.menu = result[key].menu; //add a new key named 'menu'
            listOfUser.push(result[key].data);
          }
          me.listOfAllUsers = listOfUser;
          me.onClear();
          // console.log(me.listOfAllUsers);
        })
        .catch(error => {
          console.log(error);
        });
    },
    onGetUserById(userId, callback) {
      const me = this;
      me.isRowActive = true;
      
      const url = me.url + me.verbs.user.finbyuser;
      axios
        .get(url + '/' + userId, {
          method: "GET"
        })
        .then(response => {
          callback(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    },
    resetForm(UserForm) {
      this.$validator.reset();
      for (var key in UserForm) {
        UserForm[key] = "";
      }
    },
    resetListBox() {
      this.dsSelectedItems = [];
      var listSelected = $("#listBoxSelected").data("kendoListBox");
      listSelected.remove(listSelected.items());
      
      var listItems = $("#listBoxItems").data("kendoListBox");
      listItems.dataSource.data(this.dsListItems);
      
      listItems.clearSelection();
      listSelected.clearSelection();
    },
    onReset() {
      this.resetForm(this.UserModel);
      this.resetListBox();
    },
    onClear(){
      this.action = 'add';
      this.isRowActive = false;
      this.cellSelected = '';
      this.dsSelectedItems = [];
      this.onReset();
    }
  },
  watch: {
    action: function(value) {
      if(value == 'add'){
        //Set up the inputs for adding the data
        this.isDisabled = false;
        this.isShow = true;
      }else{
        //Set up the inputs for editing the data
        this.isDisabled = true;
        this.isShow = false;
      }
    },
    isRowActive: function (bool) {
      if(bool){
        this.isAddDisabled = true;
        this.isEditDisabled = false;
        this.isDeleteDisabled = false;
        this.isResetPassDisabled = false;
      }else{
        this.isAddDisabled = false;
        this.isEditDisabled = true;
        this.isDeleteDisabled = true;
        this.isResetPassDisabled = true;
      }
    }
  }
};
</script>
<style scoped>

.table>tbody>tr.active>td {
  background-color: #123456;
  color: #fff;
}
/* .table-hover tbody tr:hover td {
  background-color: #9A0000;
  color: #fff;
} */
.modal-body {
  padding: 20px;
  max-height: calc(100vh - 180px);
  overflow-y: auto;
}
/* .modal-footer {
  margin-top: 16px;
  padding: 10px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
} */
@media (min-width: 768px) {
  .modal-dialog {
    width: 590px;
    margin: 30px auto;
  }
}
.modal-wide .modal-dialog {
  min-width: 30%;
}

.top-buffer {
  margin-top: 10px;
}
label {
  color: #000;
}
.form-group {
  margin-bottom: 10px;
}
.text-danger {
  height: 7px;
  color: #C50C03;
}
.has-error {
  border-color: none;
  /*box-shadow: none;*/
}
.highlight {
  border-color: none;
  background-color:#337ab7;
  color: #ffffff;
}
.btn-primary {
  background-color: #337ab7;
}
.btn-info {
  background-color: #269abc;
}
.btn-danger {
    background-color: #d43f3a;
}
.btn-warning {
  background-color: #eea236;
}
.modal-body {
  color: #000;
}
</style>
