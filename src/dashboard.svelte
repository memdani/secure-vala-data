<script>
    import { supabase } from './supabaseClient'
    import { user } from './sessionStore'
  
    let loading = true
    let username = null
    let website = null
    let avatar_url = null
  
    async function getProfile() {
      try {
        loading = true
        const user = supabase.auth.user()
  
        let { data, error, status } = await supabase
          .from('profiles')
          .select(`username, website, avatar_url`)
          .eq('id', user.id)
          .single()
  
        if (error && status !== 406) throw error
  
        if (data) {
          username = data.username
          website = data.website
          avatar_url = data.avatar_url
        }
        // console.log(data)
      } catch (error) {
        alert(error.message)
      } finally {
        loading = false
      }
    }

  
    // async function updateProfile() {
    //   try {
    //     loading = true
    //     const user = supabase.auth.user()
  
    //     const updates = {
    //       id: user.id,
    //       username,
    //       website,
    //       avatar_url,
    //       updated_at: new Date(),
    //     }
  
    //     let { error } = await supabase.from('profiles').upsert(updates, {
    //       returning: 'minimal', // Don't return the value after inserting
    //     })
  
    //     if (error) throw error
    //   } catch (error) {
    //     alert(error.message)
    //   } finally {
    //     loading = false
    //   }
    // }
  
    async function signOut() {
      try {
        loading = true
        let { error } = await supabase.auth.signOut()
        if (error) throw error
      } catch (error) {
        alert(error.message)
      } finally {
        loading = false
      }
      
    }
  </script>
  
 <div>
     {username}
 </div>