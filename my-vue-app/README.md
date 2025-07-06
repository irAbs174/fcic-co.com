fetch("/api/auth/login", { 
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        email: "damerchiloa@gmail.com",
        password: "@Wanrltw174"
    })
})
.then(response => {
    if (!response.ok) {
        throw new Error("Login failed: " + response.status);
    }
    return response.json();
})
.then(data => {
    // You now have access to the access token
    console.log("Access Token:", data.data.access_token);
    
    localStorage.setItem('directus_access_token', data.data.access_token);
})
.catch(error => {
    console.error("Authentication error:", error.message);
});

const token = localStorage.getItem('directus_access_token');

fetch("http://api.fcic-co.com/items/your_collection", {
    headers: {
        "Authorization": `Bearer ${token}`
    }
})
.then(res => res.json())
.then(data => console.log(data));
