<template>
  <div>
    <Header />

    <section>
      <div class="container">
        <h1>
			{{project.name}}
		</h1>

		<img src="~assets/office.jpg">

		<div class="details">
			<p>{{project.description}}</p>

			<p>Student id: {{project.student_id}}</p>
			<p>Project Duration: {{project.project_duration}} day<span v-if="project.project_duration > 1">s</span></p>
			<h2>Notes</h2>
			<p>{{project.notes}}</p>
		</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
		return {
			project: {},
		}
  },
  async created() {
		try {
			const res = await this.$axios.get("/projects/"+ this.$route.params.id);
			console.log(res.data);
			
			this.project = res.data.projects
		}
		catch (err) {
			console.log(err);
		}
	}
}
</script>

<style scoped>
	.container {
		max-width: 700px;
	}

	img {
		max-width: 600px;
	}

	.details {
		font-size: 2em;
	}
</style>