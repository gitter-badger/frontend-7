 <template>
  <div>
    <md-empty-state v-if="projects.length === 0" md-icon="devices_other" md-label="Create your first project" md-description="Creating project, you'll be able to add tasks and share it with people.">
      <md-button to="/projects/create" class="md-primary md-raised">Create first project</md-button>
    </md-empty-state>
    <md-list v-if="projects.length > 0">
      <md-list-item :key="p.id" v-for="p in projects">
        <md-icon></md-icon>
        <span class="md-list-item-text">{{p.name}}</span>
        <md-button :to="{name:'ViewProject', params: {id: p.id}}" class="md-icon-button md-list-action" title="View Project">
          <md-icon class="md-primary">create</md-icon>
        </md-button>
        <md-button :to="{name:'ViewTasks', params: {id: p.id}}" class="md-icon-button md-list-action" title="View Tasks">
          <md-icon class="md-primary">list</md-icon>
        </md-button>
        <md-button :to="{name:'TakePart', params: {id: p.id}}" class="md-icon-button md-list-action" title="Take Part!">
          <md-icon class="md-primary">forward</md-icon>
        </md-button>
      </md-list-item>

      <md-divider class="md-inset"></md-divider>

    </md-list>
  </div>
</template>

<script>
import { mapState } from "vuex"
import draggable from 'vuedraggable'
export default {
  name: "project-list",
  data() {
    return {
      userID: undefined
    };
  },
  components: {
    draggable
  },
  computed: mapState({
    projects: state => state.project.projects,
    loading: state => state.project.loading
  }),
  mounted() {
    this.$store.dispatch("project/getProjects");
    this.userID = localStorage.getItem("user_id");
  },
  methods: {
  }
};
</script>
