## Basics

![[cloudformation_template.png]]
- A cloud formation is a tool which lets you create update and delete infrastructure it AWS in a consistent and repeatable way using templates.
- Resources
	- All templates have a list of resources at,  the resources section of a cloud formation tells cloudformation what to do if resources are added to it and cloudformation creates resources, if resources are updated, then it updates those resources, if resources are removed from a template and that template and the template is re-applied then physical resources are removed.
	- The resource of section of a template is the only mandatory part of the cloudformation template.
- Description
	-  The description is a free text field which lets the author of the template to give some details about what the template does, what resources get changed, the cost of a template, anything that you want the users of a template to know you can put in the description.
	- The only restriction which you need to be aware of is if you have both format version and the description, you need to immediately follow the template format version, the template format version isn't itself mandatory but if you use them both then description needs directly follow the template format version.
- TemplateFormatVersion
	- The template format version is the way that AWS allow for extending the standards over time if it's emitted this value is assumed.
- Metadata
	- The metadata in the template has got many functions including some pretty Advanced ones but one of the things that it does is it can control how the different things in the cloud information template and presented through the console UI, you can specify groupings, control the order, add descriptions and labels. It's a way that you can force how the UI present the template. 
	- Generally the bigger your template The Wider the audience the more likely it's going to have a metadata section.
- Paramemters
	- The parameters section of the template is where you can add feels which prompt the user for different options.
	- This could be used for which size of instance to create, the name of something, the number of availability zones to use, parameters can even have settings for which are valid entries, so you apply criteria for values that can be added as parameters and you can also apply default values.
- mappings
	- This is another optional section, ii allows you to create lookup tables,eg based on region and instance type to AMI and then based on the region that it's in and then the environment type so test or prod it selects a specific machine image to use.
- Conditions
	-  These allow decision making in the template.
	- This is a two-step process, first you have to create the condition then if the condition is met then it will be used in the Resource to create things.
- Outputs
	-  There are a way, once the template is finished, to output what was created, updated or deleted etc.
## Basic workflow

The resource inside a cloudformation template are called **logical resources**.
A logical resource has a type and its the type that CF uses to know what exactly to create.
Once a template is given to CF, it creates a stack, a stack contains all of logical resources that a template asks it to create. One template could create any number of stacks.

For any logical resources in the stack, CF makes a corresponding physical resource in your AWS account. It creates logical and physical resources in sync.