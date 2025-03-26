# agents.txt

Right now, websites have a robots.txt file that specifies what pages crawlers are allowed to use. As agents' capacity to use websites becomes more sophisticated (and as acceptance of regular crawlers decreases), it is important to create systems for websites to describe how agents should interact with websites.

A good starting point is [llms.txt], which uses a Markdown file to describe information about a page in a way that LLMs can understand it. Note that llms.txt doesn't currently support permission management mechanisms.