# Access Control Models

#### Introduction to Access Control

**Access Control** is the set of mechanisms and policies that determine who can perform actions on a system or resource. It ensures that subjects (users, programs) are properly **authorized** to interact with objects (files, databases, hardware).

Access control is implemented by three fundamental security services (AAA):

1. **Authentication:** Verifying the subject's identity.
2. **Authorization:** Determining what the authenticated subject can do (this is where control models operate).
3. **Accounting:** Recording the subject's actions.

The following models define the rules and relationships used during the Authorization process.

#### The Foundational Models

These models form the historical and functional backbone of access control.

**Discretionary Access Control (DAC)**

DAC is the simplest and most flexible model, based on the **identity** of the subject and the **owner** of the object.

* **Key Characteristic: Discretion**. The owner of a resource (e.g., the user who created a file) is allowed to determine the permissions granted to other subjects.
* **Mechanism**: Typically managed through **Access Control Lists (ACLs)** or permission bits (like the `rwx` permissions in Linux).
* **Security Implication**: DAC is generally the **least secure** model because it relies on the resource owner making correct security decisions. It is prone to accidental data exposure, as permissions can be easily passed from user to user.

**Mandatory Access Control (MAC)**

MAC is the most rigid and secure model, enforced system-wide regardless of the owner's wishes.

* **Key Characteristic: Classification and Labeling**. Every subject (user) is assigned a **Security Clearance Label** (e.g., Top Secret, Secret, Confidential), and every object (data) is assigned a **Sensitivity Classification Label**. Access is granted only when the subject's label matches or exceeds the object's required label.
* **Mechanism**: The system's kernel (the **Trusted Computing Base** or TCB) strictly enforces the policy.
  * **Bell-LaPadula Model**: Focuses on **Confidentiality** (No write down, no read up).
  * **Biba Model**: Focuses on **Integrity** (No write up, no read down).
* **Security Implication:** Provides the **highest assurance** against data leakage and corruption. Used primarily in military and highly secured environments where information protection is paramount.

**Role-Based Access Control (RBAC)**

RBAC is the dominant model in modern commercial environments, providing scalability and efficient management.

* **Key Characteristic: Role**. Access permissions are organized around the **roles** (job functions) and responsibilities within an organization, not individual identities. Users are assigned to roles, and roles are assigned permissions.
* **Mechanism**: Centralized management via Identity and Access Management (IAM) systems or Active Directory. Policies can include **Separation of Duties** constraints (e.g., a "Creator" role cannot also be an "Approver" role).
* **Security Implication:** Highly **scalable** and manageable. It enforces the **Principle of Least Privilege** efficiently by ensuring users only have the permissions required for their job function.

#### Modern and Advanced Models

These models refine or extend the foundational concepts to meet complex, dynamic requirements.

**Attribute-Based Access Control (ABAC)**

* **How it Works:** Access decisions are based on the dynamic evaluation of **attributes** belonging to the user, the resource, and the environment.
* **Attributes Used:**
  * **Subject:** User's department, job title, clearance.
  * **Object:** Resource sensitivity, file type, owner.
  * **Environment:** Time of day, geographical location (IP address).
* **Security Implication:** Provides the most **granular and dynamic** access control. Often used in cloud and microservice architectures where rules must change instantly based on context.

**Rule-Based Access Control (RuBAC)**

* **How it Works:** Access is granted or denied based on a predefined set of **static, explicit rules**.
* **Mechanism:** Primarily seen in **Firewall Rules** and basic **ACLs** where simple boolean logic (permit/deny) is applied based on network criteria (source IP, destination port).
* **Security Implication:** Excellent for perimeter enforcement, but rigid compared to ABAC.

**Context- and Content-Aware AC**

* **Context-Aware AC:** Refines access based on the **environmental conditions** of the request (e.g., denying access to sensitive resources if the user is logging in from a public Wi-Fi network).
* **Content-Aware AC:** Refines access based on the **data within the resource** (e.g., blocking access to a database record if it contains more than a threshold of PII, even if the user has database access).
