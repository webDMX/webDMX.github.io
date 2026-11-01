---
layout: home
title: Welcome to webDMX on GitHub!
---

<img align="right" width="100" src="https://avatars.githubusercontent.com/u/184787984" alt="webDMX Logo">
On GitHub we host all open source code for the <a href="https://webdmx.com">webDMX</a> project.<br />
<br />

## Repositories
<div class="repo-grid" id="repo-list">
  <p>Repositories loading ...</p>
</div>

<script>
const organization = "webDMX";

fetch(`https://api.github.com/orgs/${organization}/repos?per_page=100&type=public&sort=full_name`)
  .then(response => {
    if (!response.ok) throw new Error(`GitHub API error: ${response.status}`);
    return response.json();
  })
  .then(repos => {
    const container = document.getElementById("repo-list");
    container.innerHTML = "";
    
    if (repos.length === 0) {
      container.textContent = "No public repositories found.";
    }
    else {
      repos.forEach(repo => {
        const card = document.createElement("div");
        card.className = "repo-card";
  
        const title = document.createElement("a");
        title.href = repo.html_url;
        title.textContent = repo.name;
        title.target = "_blank";
        title.rel = "noopener noreferrer";
  
        const description = document.createElement("p");
        description.textContent =
          repo.description || "No description available.";
  
        const info = document.createElement("small");
        info.textContent =
          `${repo.language || "Unknown"} · ⭐ ${repo.stargazers_count}`;
  
        card.append(title, description, info);
        container.appendChild(card);
      });
    }
  })
  .catch(error => {
    document.getElementById("repo-list").textContent =
      "Repositories could not be loaded.";
    console.error(error);
  });
</script>
