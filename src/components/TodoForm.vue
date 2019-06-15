<template>
    <v-form ref="form" v-model="valid">
        <v-container>
            <v-layout align-center>
                <v-flex xs12>
                    <v-text-field
                        v-model="todo.title"
                        label="Título"
                        required
                        :rules="titleRules"
                        >
                    </v-text-field>
                </v-flex>

                <v-btn
                    icon
                    dark
                    color="pink"
                    @click="submit"
                    :disabled="!valid">
                    <v-icon>save</v-icon>
                </v-btn>
            </v-layout>
        </v-container>
    </v-form>
</template>

<script>
export default {
  props: {
    selectedTodo: Object
  },
  data() {
    return {
      valid: false,
      todo: {
        id: "",
        title: "",
        created_by: "1"
      },
      titleRules: [
        v => !!v || "Informe um título",
        v => (!!v && v.length > 3) || "Título deve conter mais de 3 caracteres"
      ]
    };
  },

  watch: {
    selectedTodo() {
      if (this.selectedTodo) {
        const { id, title, created_by } = this.selectedTodo;
        this.todo = { id, title, created_by };
      }
    }
  },

  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        this.$emit("submited", this.todo);
      }
    }
  }
};
</script>

