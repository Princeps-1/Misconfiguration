# Misconfiguration

Once I have all the screenshots for this project - I will input all of it onto here. I need to give Defender for Cloud a day to scan and give me the recommendations for the misconfigurations I created for my storage accounts. 

## Creating the risk

I took my two storage accounts and intentionally lowered the security posture of both of them to start this task.
1. I created a Security Admin role that was assigned to a guest user. This gave them the ability to full manage both storage accounts - I am not adhering to principle of least privilege. 
2. I allowed complete public access. I was not holding back here. I am **not** restricting access to pertinent users. 
3. I allowed anonymous blob access - This removes non-repudiation!
4. I disabled secure transfer - Confidentiality of the CIA triad is not being met!
5. I also lowered the minimum encryption standard to TLS 1.0 - as we know this is a catastrophe waiting to happen.
6. I did not use Key Vault to store my keys - I will not be rotating them and I will allowed shared key access.
  
  
  
   <img width="1055" height="701" alt="Defender Alert 1 for Storage Account" src="https://github.com/user-attachments/assets/a29501c0-6820-464d-98f7-5154e87aa7cc" />

   <img width="693" height="582" alt="Storage Account Key Rotation" src="https://github.com/user-attachments/assets/1ad1fab4-ff7d-49a7-8fca-08e55588340c" />

   <img width="1602" height="617" alt="Insecure Storage " src="https://github.com/user-attachments/assets/35477605-3e77-4e45-8cf6-239984112483" />


   All of the above was done to help me understand how these threats would look in a real time environment and it would also replicate what I see at work.


I had to let Defender scan this. I waited a day in order for it to pickup that I had created another Storage Account. 

   <img width="761" height="342" alt="Storage Account Full list of recommendations" src="https://github.com/user-attachments/assets/c7eb54c0-5e88-40c5-9fec-b3f475d6d075" />
  As you can see, I do not have premium Defender for Cloud enabled currently so it will not give me a risk evaluation. I have subscribed to a premium plan below and had to wait a short time for it to activate and scan my environment. 

   <img width="1602" height="616" alt="image" src="https://github.com/user-attachments/assets/135cf45d-3130-4258-bd85-6ac835c76fe8" />

## Evaluating and rectifying the risk

In my environment, I have 1 Critical risk, 1 High risk, 1 Medium risk and lots of Low risks. 
I will go through the risk in order of highest severity:

   <img width="1873" height="740" alt="image" src="https://github.com/user-attachments/assets/b78af674-d579-4aa6-8a57-4a14dd2364e3" />

A public facing storage account will never be needed so an exemption is out of the question. I would be violating many basic rules of Cybersecurity by disregarding this. I remedy this by turning off 'Anonymous Blob Storage Access' in the Networking section of the storage account.


   <img width="1898" height="830" alt="image" src="https://github.com/user-attachments/assets/c2f7e75e-3a0c-40f3-a20d-b6d3d030d104" />

Microsoft recommends authorising requests using Azure AD as a key can be shared and access by others, whilst authenticating to Azure AD is far more difficult. It also makes it simpler by removing the need for a key entirely. 

   <img width="1887" height="747" alt="image" src="https://github.com/user-attachments/assets/5f444228-9dcf-4d67-8b6b-3b996e285617" />

  This one relates to my other storage account. In this case, I can click on 'Exempt' and remove this, should the situation call for it. Even then, it needs to be agreed upon and an exception RECORDED in a list. 
  For my purposes, I have no need for a publicly accessible storage account, so I will disable it. 

The rest of the alerts are all Low and after going through and remedying some of them I have decided that some of them can be safely ignored. 
This includes and is not exclusive to:

- Activating MS Defender on servers
- Using a private link connection
- Windows Virtual Machines should enable Azure Disk Encryption or EncryptionAtHost

## Post Remediation Scan


  
