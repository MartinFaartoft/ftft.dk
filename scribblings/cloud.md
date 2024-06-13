# Cloud ☁️
2023-08-19

For the last decade, I have been building and operating large, distributed systems.
During this period, cloud services have become the de-facto standard for systems, big and small. But doing cloud well, without breaking the bank is hard.

Here are my top tips for cloud.

👉 Script your Cloud resources with Infrastructure as Code (IaC)
Keeping environments clean and identically configured is easy if you script it, and exhausting if you try it with only the web interface.

There are also a handful of good tools, that will scan your cloud scripts and warn you about misconfigurations, without any access to your cloud accounts.

👉 Decide on a resource naming scheme and stick to it
- Make it easy for humans to understand (have prod in the name if it's a prod resource)
- Make it consistent and easy to template, so you don't need separate copies of dashboard and alert definitions.

Be aware of the limitations (max length, alpha-numeric only, globally unique), so you don't hit a late roadblock, trying to provision "ecommerce-service-prod"

👉 Use the principle of 'Least Privilege' for access control
- No cross-environment access
- No cross-service access within an environment

If your dev environment IaC account cannot access production, it cannot accidently mess it up.
If a dev account gets compromised, it's not trivial for an attacker to escalate access to prod

Bonus points for making prod read-only to human accounts, meaning all changes must be done through IaC.

👉 Monitor cost
Cloud providers make it easy to spend more than you expect.
If you have a way to see how cost evolves over time, it's easy to catch the experimental resource that was forgotten, or the service that was temporary scaled up to handle a load spike

Many stateful cloud resources allow you to set up policies for when data should be automatically deleted, or moved to a cheaper tier. If applied consistently, no single resource spend should be growing unbounded over time. 

👉 Take the word "managed" with a large grain of salt
Even if the cloud provider takes care of keeping the thing running, you should read the fine print and understand what is required on your end. There's usually a little maintenance and a lot of expertise required by you, to keep the resource running well in the long run.