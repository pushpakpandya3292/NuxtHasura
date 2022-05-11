<script>
import gql from 'graphql-tag'

export default {
  name: 'CharacterCard',
  apollo: {
    // Dynamic querying
    character: {
      query: gql`
        query getCharacter($id: ID!) {
          character(id: $id) {
            id
            name
            status
            species
            gender
            image
            origin {
              name
            }
          }
        }
      `,
      variables() {
        return {
          // if the route.params.id is null make id = 1
          id: this.$route.params.id || 1,
        }
      },
    },
  },
}
</script>