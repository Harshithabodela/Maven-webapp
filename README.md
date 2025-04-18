
To set up a CI/CD pipeline that pulls code from GitHub, builds it using Maven, and automatically deploys the generated WAR file to an Apache Tomcat server hosted on an AWS EC2 instance using Jenkins

### ✅ What We Did:

1. Created an EC2 instance** (Amazon Linux 2) and connected via MobaXTerm.

2. Installed Jenkins**:
   - Added Jenkins repo and installed it via YUM.
   - Installed Java 11 (required by Jenkins).
   - Started Jenkins on default port 8080 and set it up via web browser.
   - Opened port 8080 in EC2 Security Group for browser access.

3. Installed Apache Tomcat 9**:
   - Downloaded and extracted Tomcat.
   - Changed default port from 8080 to **9090** to avoid conflict with Jenkins.
   - Started Tomcat and opened port 9090 in the Security Group.

4. Configured Tomcat**:
   - Enabled full access to the Tomcat manager app.
   - Added users with `manager-gui`, `admin-gui`, and `manager-script` roles for deployment access.

5. Installed Git** on the EC2 instance (required for Jenkins to pull code).

6. Installed required Jenkins plugins**:
   - `Deploy to container` plugin for WAR deployment to Tomcat.

7. Configured Jenkins Tools**:
   - Set up Java, Git, and Maven in Jenkins Global Tool Configuration.

8. Created a Jenkins Freestyle Project**:
   - Connected to a GitHub repo: `https://github.com/KastroVKiran/Internship-Studio-MavenWebApp.git`
   - Configured build step to run `mvn clean package`.
   - Configured post-build step to deploy WAR file to Tomcat using manager-script credentials.

9. Set up GitHub Webhook**:
   - Triggered Jenkins build on every push to GitHub using GitHub webhook (`http://<Jenkins-IP>:8080/github-webhook/`).

---

### 🌐 Ports Used:
- **Jenkins**: 8080  
- **Tomcat**: 9090  

---

### 🚀 Final Result:
Whenever code is pushed to the GitHub repo, Jenkins:
- Pulls the latest code.
- Builds it with Maven.
- Generates a `.war` file.
- Deploys it to the Tomcat server on port 9090 — all automatically.

---

