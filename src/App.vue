<template>
  <div id="app">
      <h1>Add note</h1>
<form @submit.prevent="add_note" class="form-group container">
  <div class="col mb-3">
    <label for="note" class="form-label">Note </label>
    <input type="note" id="note" v-model="note" class="form-control">
  </div>
  <div>
    <label for="category" class="form-label">Category </label>
    <select class="form-select" id="category" v-model="category">
      <option value="personal">personal</option>
      <option value="work">work</option>
      <option value="study">study</option>
      <option value="family">family</option>
      <option value="other">other</option>
    </select>
  </div>

  <label class="form-label">Priority</label>
  <div>
    <input type="radio" class="form-check-input" value="high" id="high" v-model="priority">
    <label class="control-label" for="high">high</label>
  </div>
  <div>
    <input type="radio" class="form-check-input" value="medium" id="medium" v-model="priority">
    <label class="control-label" for="medium">medium</label>
  </div>
  <div>
    <input type="radio" class="form-check-input" value="low" id="low" v-model="priority">
    <label class="control-label" for="low">low</label>
  </div>
  <input type="submit" value="Add" class="btn btn-primary mt-2" />


</form>
<h1>Notes</h1>
<button @click="reset_notes" class="btn btn-primary mt-2">Reset</button>
<div>
<table class="table">
  <thead>
    <tr>
      <th scope="col">№</th>
      <th scope="col">note</th>
      <th scope="col">category</th>
      <th scope="col">priority</th>
      <th scope="col">done</th>
    </tr>
  </thead>
  <tbody v-for="(note, index) in this.notes" :key="index">
    <tr>
      <td>{{ index }}</td>
      <td>{{ note.note }}</td>
      <td>{{ note.category }}</td>
      <td>{{ note.priority }}</td>
      <td>{{ note.done ? 'yes ' : 'no ' }}<input type="checkbox" v-model="note.done" class="form-check-input"/></td>
    </tr>
  </tbody>
</table>
</div>
</div>
</template>

<script>
export default {
  data() {
    return {
      note: '',
      category: 'personal',
      priority: 'low',
      done: false,
      notes: JSON.parse(localStorage.getItem('notes')) || [],
      
    };
  },

  methods: {
    add_note() {
      const new_note = {
        note: this.note,
        category: this.category,
        priority: this.priority,
	done: this.done,
      };

      this.notes.push(new_note);
      this.save_note();
      this.note = '';
      this.category = 'personal';
      this.priority = 'low';
      this.done = false;
    },

    save_note() {
      localStorage.setItem('notes', JSON.stringify(this.notes));
    },

    reset_notes() {
      localStorage.removeItem('notes');
      this.notes = [];
    },
  },
};
</script>
<style>
#app {
  text-align: center;
}
</style>
