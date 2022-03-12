<!-- TODO: Rewrite from Vuelidate example: https://vuetifyjs.com/en/components/forms/#vuelidate -->
<template>
	<form style="margin=30%">
		<v-text-field
      v-model="user.firstname"
      :error-messages="firstNameErrors"
      label="First Name"
      required
      @input="$v.firstname.$touch()"
      @blur="$v.firstname.$touch()"
    ></v-text-field>
		<v-text-field
      v-model="user.lastname"
      :error-messages="lastNameErrors"
      label="Last Name"
      required
      @input="$v.lastname.$touch()"
      @blur="$v.lastname.$touch()"
    ></v-text-field>
    <v-text-field
      v-model="user.email"
      :error-messages="emailErrors"
      label="E-mail"
      required
      @input="$v.email.$touch()"
      @blur="$v.email.$touch()"
    ></v-text-field>

		<v-btn
      class="mr-4"
      @click="submit"
    >
      submit
    </v-btn>
    <v-btn @click="clear">
      clear
    </v-btn>
	</form>
</template>

<script>
	import { validationMixin } from 'vuelidate'
	import { required, email } from 'vuelidate/lib/validators'

	export default {
		mixins: [validationMixin],

		validations: {
			firstname: { required },
			lastname: { required },
			email: { required, email }
		},

		data() {
			return {
				user: {
					firstname: '',
					lastname: '',
					email: ''
				}
			}
		},

		computed: {
			firstNameErrors () {
        const errors = []
        if (!this.$v.firstname.$dirty) return errors
        !this.$v.firstname.required && errors.push('First name is required.')
        return errors
      },
			lastNameErrors () {
        const errors = []
        if (!this.$v.lastname.$dirty) return errors
        !this.$v.lastname.required && errors.push('Last name is required.')
        return errors
      },
      emailErrors () {
        const errors = []
        if (!this.$v.email.$dirty) return errors
        !this.$v.email.email && errors.push('Must be valid e-mail')
        !this.$v.email.required && errors.push('E-mail is required')
        return errors
      }
		},

		methods: {
			submit () {
				alert(JSON.stringify(this.user)) 
			},
			clear () {
				this.$v.$reset()
				this.firstname = ''
				this.lastname = ''
				this.email = ''
			}
		}
	}
</script>
