Microsoft Entra is a unified Identify and Access management (IAM) solution developed by Microsoft designed to help organization secure identies across cloud, Hybrid or on premises resources. Entra enables organizations to magage who has access to what Under what circumstances and ensure most people have it. This is The rebranding of Azure Active Directory. 


### Key Components of Microsoft Entra:

1. **Microsoft Entra ID (formerly Azure Active Directory - Azure AD)**:
    
    - This is the core identity and access management service in Microsoft Entra. It provides:
        - **Single Sign-On (SSO)**: Allows users to sign in once and access multiple applications without re-entering credentials.
        - **Multi-Factor Authentication (MFA)**: Adds an extra layer of security by requiring users to verify their identity with a second factor, such as a mobile app or SMS.
        - **Conditional Access**: Policies that allow or block access to resources based on specific conditions, such as user location, device, or application.
        - **Identity Protection**: Detects risky sign-ins and helps mitigate threats by applying automated responses to high-risk accounts.
2. **Microsoft Entra Permissions Management**:
    
    - A solution focused on managing and governing access to resources across multiple cloud platforms, such as Azure, AWS, and Google Cloud. It allows organizations to enforce least-privileged access by providing insights into permissions usage and access anomalies.
3. **Microsoft Entra Verified ID**:
    
    - This component enables the issuance and verification of decentralized digital identities. It is based on verifiable credentials, allowing organizations to issue digital identity credentials that individuals or entities can control and present securely when needed.
    - Examples include verifying employees' work credentials or confirming identity in secure transactions without traditional identity proofing methods.
4. **Microsoft Entra Workload Identities**:
    
    - Manages the identities of apps, services, and virtual machines, ensuring secure authentication and access management for non-human entities (workloads).
    - This component helps secure communications between services, automates credential management, and enforces security policies for non-human identities.
5. **Identity Governance**:
    
    - Microsoft Entra also includes features for governing and auditing access to resources. It helps organizations ensure compliance with regulatory requirements and corporate policies by managing lifecycle access, reviewing permissions, and enforcing role-based access controls (RBAC).



Entra doesnt use Kerberos in most Cloud environments by default it the primary protocols used for SSO in ENTRA ID are 

OAuth 2.1

OpenID connect (OIDC)


SAML (Security Assertion Markup Language)


WS-Federations 



Although in Hybrid Environments you may see both Microsoft Entra and Kerebos being used. 