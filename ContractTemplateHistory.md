This repository of the Human Dynamics Lab was started for the purpose of containing legal documents in template format intended eventually to be usable for deployments of openPDS, FUNF and other open source code from or used by this research lab.  The following high level approach to use of a template to generate final legal agreements and notices code was created and crafted by Brian Sweatt in collaboration with Dazza Greenwood. Dazza requested feedback on how best to:

> 1. Setup and use a Human Dynamics Repository to house a re-usable set of legal agreements for deployments of openPDS and other relevant projects, such that, for example, the upcoming DTU 1,000 Phone study can draw from a common general set of files and thereby leverage and contribute back to the broader community of implementers collaborating on Human Dynamics Lab and related research and development;

> 2. Use a parameter and value approach to the names of parties and references to the types of resources and obligations or rights included in the legal file (eg to use "data_owner" and "service_provider" using existing widely accepted standards like Dublin Core, NEIM and the US-Code, and including a standard reference file where the actual names of the parties and OAuth2 Scopes or other content fields would be filled in), and;

> 3. Describe and apply the New Deal on Data from the vantage point of it's legal and policy essential elements and thereby provide a benchmark against with to evaluate the extent to which future deployments and other systems support and reflect the New Deal on Data. 

Brian immediately recognized items 1 and 2 above as a "template" functionality and jumped right into a text document to "talk with his code" and hack out the fundamental approach to accomplish this.  Careful to indicate that there are many different template languages and approaches, Brain demonstrated how this might be done at a conceptual level using Python and Django, highlighted how this would be quite similar with other implementations (eg Mustache) and illustrated who use of "control statements" would then provide even more robust template-driven functionality but at the same time limit the parsing engines that are capable of computing the code (ie, basically requiring a Django parser to interpret the control statements and a very different approach if Java or code contexts).  

The starting point, late on the afternoon of August 5th, 2013, was the original hack below, by Brain (including his apt and resourceful disclaimer, added as the last edit to the file!):

> Pasted verbatim from the little text file I threw together during our discussion.

> Disclaimer: this is an example, and shouldn't be expected to actually run or do anything useful. 

> contract_template.txt

> I, {{ data_owner }} hereby grant {{ institution }} access to the following data:

> {% for scope in scopes %}
>   {{ scope }}
> {% endfor %}

> # OR

>   {{ scope1 }}
>   {{ scope2 }}
>   {{ scope3 }}


> MIT_template.json:

> {
>   "data_owner": "Brian Sweatt", 
>   //"scopes": [ "location", "contacts", "activity" ],
>   "institution": "MIT",
>   "scope1": "location", 
>   "scope2": "contacts"
> }

> README:

> TO generate your contract, run this:

> ./template-parser contract_template.txt MIT_template.json > contract.txt


The above hack is the starting point for the approach being following in this Repository. 

Game On.
