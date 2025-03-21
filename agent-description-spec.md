**Description:**
A standardized format is essential for describing the metadata and capabilities of agents. This specification should provide an appropriate level of abstraction to ensure interoperability across various agent frameworks and programming languages.

# **Problem Statement**
Agent metadata is essential for enabling discovery of intelligent agents. The lack of a standardized mechanism for describing agent metadata leads to fragmentation, making interoperability between different programming languages and platforms challenging. 
We need the analogy of metadata files used in Helm charts and package managers for agents.  

# **Key Benefits**
1. **Discovery:** Enables agents to discover each other based on their capabilities.
2. **Version Management:** Provides versioning details to manage updates.
3. **Security and Compliance:** Specifies authentication, encryption and compliance capabilities.
4. **Autonomy:** Empowers agents to make autonomous decisions based on metadata.

# **Requirements**
## **1. Standardized Metadata Representation**
- Define a machine-readable format (e.g., JSON, JSON-LD) for agents and tools to describe their capabilities and interfaces.
- It must be possible to sign the description document so that it is verifiable 
- Ensure extensibility to accommodate future enhancements.
- Include core metadata attributes such as:
  - Unique agent identifier
  - Functional capabilities
  - Authentication and security attributes
  - Version information

## **2. Dynamic Discovery and Metadata Propagation**
- Implement mechanisms for agents to dynamically register and propagate their metadata.
- Support real-time, run-time discovery of other agents.

# **Discovery Mechanism Options**
1. **Centralized Registry**
   - Agents publish metadata to a central registry.
   - Enables efficient querying and retrieval of agent details.
   
2. **Local Network Discovery**
   - Utilize protocols like mDNS (Multicast DNS) for agent metadata propagation in local networks.
   - Facilitates low-latency peer discovery within restricted environments.
   
3. **Decentralized, federated Networks**
   - Decentralized discovery mechanism where agents share metadata directly with peers or federated registries.
   - Eliminates reliance on a central authority.

# **Expected Outcome**
- A standardized description format for intelligent agents.
- A discovery protocol that supports real-time registration and querying of agents.
- Interoperability across diverse platforms and implementations.

# Proposed Solution
## 1. Use JSON-LD (JavaScript Object Notation for Linked Data).
[Eclipse LMOS protocol](https://eclipse.dev/lmos/docs/lmos_protocol/agent_description/) and [Agent Network Protocol](https://agent-network-protocol.com/specs/agent-description.html) are already using JSON-LD for this format. 
JSON-LD is a JSON-based format designed to serialize Linked Data, enabling data to be interlinked and semantically enriched. 

Side note: [W3C DID](https://decentralized-id.com/) could be used to authenticate agents and could also be used to sign metadata and verify metadata.

[W3C Web of Things](https://www.w3.org/TR/wot-thing-description11/) is calling the following document a Thing Description and has specifications for Discovery and also supports Security Schemes like Bearer, Oauth2, and many more.

Thw following is an example based on the WoR format with extensions. A thing description uses Links to point to further documents or can include metadata directly into the document.

```
{
   "@context": [
      "https://www.w3.org/2022/wot/td/v1.1",
      {
         "ad": "https:/las-wg/protocol/agent-description/v1",
      }
   ],
   "@type": "ad:Agent",
   "id": "did:web:vendor.com:6f1d3a7a-1f97-4e6b-b45f-f3c2e1c84c77",
   "version": "1.0.0",
   "created": "2018-11-14T19:10:23.824Z",
   "modified": "2019-06-01T09:12:43.124Z",
    "titles": {
        "en": "MyAgent",
        "de": "MeinAgent",
        "ja": "私の物",
        "zh-Hans": "我的东西", 
        "zh-Hant": "我的東西"
    },
    "descriptions": {
        "en": "Human readable information.",
        "de": "Menschenlesbare Informationen.",
        "ja": "人間が読むことができる情報",
        "zh-Hans": "人们可阅读的信息", 
        "zh-Hant": "人們可閱讀的資訊"
    },
   "links": [{
      "rel": "service-doc",
      "href": "https://vendor.com/capabilities.json",
      "type": "application/json",
      "hreflang": "en"
   }],
   "ad:metadata": {
        "ad:vendor": {
            "ad:name": "Vendor A",
            "ad:url": "https://vendor.com"
        }
   }
    "support": "mailto:support@example.com",

    "securityDefinitions": {
        "basic_sc": {
            "scheme": "basic",
            "in": "header"
        }
    },
    "security": "basic_sc"
   ....
}
```

## 2. Markdown + Yaml Frontmatter
Huggingface is using markdown and yaml frontmatter for Model Cards: https://huggingface.co/docs/hub/model-cards

