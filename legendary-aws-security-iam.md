<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Cloud Security with AWS IAM

**Project Link:** [View Project](http://nextwork.ai/projects/aws-security-iam)

**Author:** Francesca Danielle Pueyo  
**Email:** supamimingsshow@gmail.com

---

![Image](http://nextwork.ai/sincere_rose_zesty_sea_urchin/uploads/aws-security-iam_1c864649)

---

## Introducing Today's Project!

### Project overview

We are here to launch two EC2 instances (one for production, one for development) and configure an AWS IAM Policy, User Group, and User to give an incoming intern permission to manage the development environment while securely blocking them from modifying the production environment.

### Tools and concepts

In this project, I mastered core AWS identity management and security principles by working directly with **AWS IAM (Identity and Access Management)**. I learned how to draft custom **JSON Policies** using **Effect, Action, and Resource** blocks to enforce least-privilege access, and I saw how creating an **Account Alias** simplifies team login workflows. By setting up **IAM Users** and **User Groups**, I figured out how to streamline permission management at scale, safely onboarding an intern while utilizing resource tags to automatically grant access to development environments while strictly blocking production tampering.

### Project reflection

It took me about 45 minutes to complete this entire project from start to finish. The initial setup of the custom JSON policies, user groups, and the account alias went smoothly, but I spent a good portion of that time carefully logging in as the new intern and testing the EC2 instances to verify that my security boundaries were actually working exactly as intended.

---

## Tags

### What I did in this step

In this step, I am launching two Amazon EC2 virtual servers to boost NextWork's computing power for the upcoming holiday traffic. I'm also adding specific tags—one labeled for production and one for development—so we can organize them and control user access based on those environments later on.

### Understanding tags

Tags are labels that I attach to my AWS resources, consisting of a key and a value like `Env: production`.

They are incredibly useful because they let me organize my infrastructure, filter resources easily when searching, track and allocate costs accurately, and apply security policies based on the specific environment type.

### My tag configuration

For my first instance, which is for the live environment, I assigned the Name tag as `nextwork-prod-[MyName]` and the Env tag with a value of `production`.

For my second instance, which is for testing and debugging, I assigned the Name tag as `nextwork-dev-[MyName]` and the Env tag with a value of `development`.

![Image](http://nextwork.ai/sincere_rose_zesty_sea_urchin/uploads/aws-security-iam_2e0e5a5d)

---

## IAM Policies

### What I did in this step

In this step, we are creating a custom IAM policy using a JSON editor to establish secure access rules for our incoming intern. This policy explicitly grants permissions to manage EC2 instances tagged as development while denying the ability to modify production instances or alter tags.

### Understanding IAM policies

IAM policies define the exact permissions for my AWS identities by using JSON documents to dictate who can access what. By attaching these policies to my users or groups, I control whether to allow or deny specific actions on specific resources, effectively acting as the ultimate gatekeeper for my cloud environment.

### The policy I set up

I set up my policy directly using **JSON**.

Writing the code by hand gave me absolute control over the exact syntax, allowing me to explicitly define the `Effect`, `Action`, and `Resource` elements. This ensured I could lock down permissions precisely to target specific environment tags and protect my production instances.

### Policy effect

My policy allows me to fully manage and control any EC2 instances that are tagged for the development environment, while completely blocking access to the production environment. It also lets me view all instances so I can see what is running, but it explicitly denies the ability to create or delete tags on any resource.

### Understanding Effect, Action, and Resource

In my JSON policy, Effect determines whether the rule grants an absolute Allow or a Deny for a request. Action defines the specific AWS operations or API calls being managed, such as starting or stopping an EC2 instance. Resource points directly to the specific AWS objects that these rules apply to, using an asterisk when the rule should cover all resources within that scope.

---

## My JSON Policy

![Image](http://nextwork.ai/sincere_rose_zesty_sea_urchin/uploads/aws-security-iam_1c864649)

---

## Account Alias

### What I did in this step

In this step, we are creating a custom AWS Account Alias to simplify the login process. By replacing the long, 12-digit AWS account number with a friendly, recognizable name, we are making the console sign-in URL much easier to remember and share with our team members.

### Understanding account aliases

An Account Alias is a custom, user-friendly name that replaces your default 12-digit AWS Account ID in your sign-in link. It turns a long, random string of numbers into a recognizable web address, making it much simpler for you and your team to remember and use when logging into the AWS Management Console.

### Setting up my account alias

Setting up my Account Alias took less than a minute. It only required navigating to the IAM dashboard, clicking "Create" under the Account Alias section, typing in my preferred custom name, and saving it to instantly update my login URL.

![Image](http://nextwork.ai/sincere_rose_zesty_sea_urchin/uploads/aws-security-iam_0eb4439b)

---

## IAM Users and User Groups

### What I did in this step

In this step, we are setting up the structure to onboard our new intern by creating an IAM User Group and an IAM User. First, we create a dedicated group called `nextwork-dev-group` and attach our custom development policy to it, and then we create the individual intern user account, assign it console login credentials, and place it directly into that group so it automatically inherits the right permissions.

### Understanding user groups

IAM user groups are collections or folders of individual IAM users. They allow me to assign and manage permission policies for multiple team members all at once, meaning any user I place inside a group automatically inherits the exact access rules attached to that group.

### Attaching policies to user groups

By attaching my policy directly to the user group, the security rules automatically apply to every single user inside that group. This means my new intern—and any future interns I add—instantly inherits the permissions to manage development instances while remaining securely blocked from touching production resources, without me needing to configure each user profile individually.

### Understanding IAM users

IAM users are individual accounts created inside my AWS account, representing a specific person or application that needs to interact with my cloud resources. Each user gets their own unique login credentials—like a password for the AWS Console or access keys for programmatic tasks—so I can track their specific activity and control exactly what they are allowed to do.

---

## Logging in as an IAM User

### Sharing sign-in details

I can share my new user's sign-in details by downloading the CSV file containing their username and password directly from the final creation screen to send it securely, or I can copy the sign-in URL alongside their credentials and email or message those details straight to them.

### Observations from the IAM user dashboard

When I logged into the console as my new intern user, I saw the standard AWS dashboard, but with clear signs that my security boundaries were working perfectly.

When I went to the EC2 dashboard, I could see both instances listed, but as soon as I tried to perform actions, the difference was immediate. I was able to stop the development instance without any issues. However, the moment I tried to stop the production instance, AWS blocked me completely and popped up an explicit API authorization error, showing me that my custom policy successfully slammed the door on any production access.

![Image](http://nextwork.ai/sincere_rose_zesty_sea_urchin/uploads/aws-security-iam_6f2ab446)

---

## Testing IAM Policies

### What I did in this step

In this step, we are putting our security configuration to the test by logging out of our main administrator account and signing back in as the new intern using our custom account alias link. Once logged in, we are intentionally trying to stop both the development and production EC2 instances to verify firsthand that our custom JSON policy successfully allows us to control development while strictly blocking us from touching production.

### Testing policy actions

The specific action I performed on both of my EC2 instances was attempting to **Stop** them. I initiated this command to test the boundaries of my custom policy, which successfully allowed me to shut down the development instance but completely blocked me from stopping the production instance.

### Stopping the production instance

The moment I tried to stop the production instance, AWS blocked me instantly and flashed an explicit API authorization error message across the top of the screen. Even though I could see the instance listed on the dashboard, the system completely refused to execute the command, proving that my custom policy successfully slammed the door on any unauthorized production access.

![Image](http://nextwork.ai/sincere_rose_zesty_sea_urchin/uploads/aws-security-iam_0e7a9d6a)

### Stopping the development instance

When I tried to stop the development instance, the action went through flawlessly and the instance began shutting down immediately without any errors. Since my custom policy specifically grants full management power over any resources tagged for the development environment, AWS recognized my permissions and let me successfully stop the instance.

![Image](http://nextwork.ai/sincere_rose_zesty_sea_urchin/uploads/aws-security-iam_1811801c)

---

## IAM Policy Simulator

### Understanding the IAM Policy Simulator

### How I used the simulator

---

---
