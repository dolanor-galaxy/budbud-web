<script>
  import { faSignOutAlt } from '@fortawesome/free-solid-svg-icons'

  import { gql } from 'apollo-boost';
  import { mutate, getClient } from 'svelte-apollo';
  import { navigate } from "svelte-routing";
  import { user } from "../stores.js";

  import Card from "../components/Card.svelte";
  import Button from "../components/Button.svelte";

  function doLogout() {
    mutate(getClient(), {
      mutation: gql`mutation{logout(none:true)}`,
    }).then(()=>{
      user.set({loggedin: false})
      navigate("/")
    })
  }
</script>
<div class="w-4/5 max-w-md mx-auto">
  <Card>
    Email: {$user.email}
    <Button onclick={doLogout} icon={faSignOutAlt} text="Logout" color="red" wfull></Button>
  </Card>
</div>