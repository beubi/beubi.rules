---
currentMenu: sf2
---

# ** Symfony2 Guidelines **

## <a name="Routing"></a>Routing

Routing is being configured through annotation like:
```
@Route("/something", name="somename")
@Method("GET/POST/DELETE")
```
Where name should be something meaningful for the business/domain plus controller name

Parameter Conversion
Whenever we have an id that is being pass to a controller as parameter but we want to use the class instead:
```
@ParamConverter("Classname", class="BeubiBundle:Classname", options={"id" = "thing-id"})
```

## <a name="Templating"></a>Templating

Templates are place under Resources/views and are injected in controllers as services.
Their paths should be given like this:
```
@Template("BeubiBundle:Thing:index.html.twig")
```
This means that no controller should return Response, but an array instead.

## <a name="Entities"></a>Entities

Documentation for gedmo extensions
https://github.com/Atlantic18/DoctrineExtensions/tree/master/doc
Documentation for doctrine
http://docs.doctrine-project.org/projects/doctrine-common/en/latest/reference/annotations.html

Annotations in entities are being used for mapping with database,

IDs must be like
@ORM\Id
@ORM\Column(type="integer")
@ORM\GeneratedValue(strategy="IDENTITY")

#### Timestampable fields / entities
You must create "set" methods of timestampable fields.
This will improve testability and turn the creation of reallife like fixtures possible.

#### CreatedAt
"createdAt" property should be set in constructor through "setCreatedAt" method like:

```
public function __construct()
{
        $this->setCreatedAt(new \DateTime());
}
```
that method shall be something like:

```
public function setCreatedAt(\DateTime $createdAt)
{
        $this->createdAt = $createdAt;
        return $this;
}
```

#### UpdatedAt
"updatedAt" property should be set in constructor through "getUpdatedAt" method like:

```
public function getUpdatedAt()
{
        return $this->updatedAt;
}
```
that method shall be something like:

```
public function setUpdatedAt(\DateTime $updatedAt)
{
      $this->updatedAt = $updatedAt;
      return $this;
}
```


#### Soft Delete

```
public function isDeleted()
{
    return null !== $this->deletedAt && new \DateTime() >= $this->deletedAt;
}

public function getDeletedAt()
{
    return $this->deletedAt;
}

public function setDeletedAt(\DateTime $deletedAt)
{
    $this->deletedAt = $deletedAt;
    return $this;
}
```

#### Making sure a field match a string
```
@Assert\Choice(callback={"Beubi\Bundle\Provider\ThingProvider","getThingTypeKeyChoices"})
```
#### Strings
Each string field should have the minimum necessary length.
When it is not possible to know this minimum length use:
medium size strings should be like (e.g. used in input field):
```
 @ORM\Column(type="string", length=200)
 ```
the biggest size strings should be like  (e.g. used in textarea field):
```
 @ORM\Column(type="string", length=255)
```

#### Files
When uploading files to register that in db we are placing this
```
@Vich\Uploadable
```
in the entity, and then this
```
@Assert\File(maxSize="5M", mimeTypes = {"application/pdf", "application/x-pdf"})
```
At `$file` property where we are asserting file max-size and mime-types

#### Inheritances
We must use when the target tables are alike
```
@ORM\InheritanceType("JOINED")
@ORM\DiscriminatorMap({"Thing" = "Thing", "AnotherThing" = "AnotherThing")
```
And
```
@ORM\InheritanceType("SINGLE_TABLE")
@ORM\DiscriminatorMap({"file" = "File", "attachment" = "Attachment", "photo" = "Photo"})
```
When target tables are different from each other (e.g. from Intervener and Attachment)

## <a name="Naming"></a>Naming

### Variables
**Prohibited** names for variables;
`form`
`entity`

### Controller methods
Every controller method must end with "Action"

**Standard controller actions**
`index`
the main method of a controller
`edit`
returns form
`update`
returns redirect, flash msg
`show`
returns an 'object' properties
`list`
return a list of 'objects' with their properties
`delete`
returns redirect, flash msg
`create`
redirects or returns a view with create form
`new`
returns view with form


### Entity methods
Names of method that return a boolean must start with "is..." or "has..."
Names of method that changes a property must start with "set..."
Names of method that returns a property must start with "get..."

### Entity properties
Properties must be in English.
No abbreviations are allowed.
When properties are ManyToOne relations they should match the class name.
e.g. "user"
When properties are OneToMany relations they should match the class name and be in plural.
e.g. "attachments"
When needed, doc block should have the field name in Portuguese.
e.g. "whoCheckedTheBuilding" ~> "Quem realizou o levantamento?"

Word list
* step
* finish
* process
* note
* attachment
* stepName
* user
* createdAt
* updatedAt
* deletedAt
* zipCode
* email
* address
* plot

Entity creation and behavior

It must not be possible to create an "invalid" Entity.

## <a name="Security"></a>Security

Security rules are being used like this:
```
@Security("has_role('ROLE_AUTH')")
```
you can also
```
@Security("is_granted('edit', step)")
```
It can be used for a whole class or a single controller.
And it must be present for every rout but "/" - homepage (login page)

### <a name="Roles"></a>Roles

Symfony documentation about security component
http://symfony.com/doc/current/book/security.html

We should use names like:

* ROLE_THING_CANCEL                          |
* ROLE_THING_CHANGE_ANOTHERTHING
* ROLE_SEARCH_BY_THING
* ROLE_THING_ACCESS
* ROLE_THING_EDIT
* ROLE_THING_DELETE                          

### Use examples

Calling service
```
$this->container->get('security.context')->isGranted('ROLE_AUTH')
```
From annotations
```
@Security("has_role('ROLE_AUTH')
```

### Voters
All voters are called each time you use the isGranted() method on Symfony's security context (i.e. the security.context service). Each one decides if the current user should have access to some resource.
To create a custom Voter, you need to implement 3 methods:
* `public function supportsAttribute($attribute);`
Check if the voter supports the given user attribute (i.e: a role like ROLE_USER, an ACL EDIT, etc.).
* `public function supportsClass($class);`
Check if the voter supports the class of the object whose access is being checked.
* `public function vote(TokenInterface $token, $object, array $attributes);`
    * Method must implement the business logic that verifies whether or not the user has access. This method must return one of the following values:
        * VoterInterface::ACCESS_GRANTED: The authorization will be granted by this voter;
        * VoterInterface::ACCESS_ABSTAIN: The voter cannot decide if authorization should be granted;
        * VoterInterface::ACCESS_DENIED: The authorization will be denied by this voter.

http://symfony.com/doc/current/cookbook/security/voters_data_permission.html#creating-the-custom-voter

## <a name="Enumerations"></a>Enumerations (choices)

A provider must be created for each enumeration.
This provider must have one constant properties for each possible choice and an array calling this constants.
This provider must implement a getTypeChoices() method which will return the possible choices.
This choices should be in form of "choices.<<providerName>>.<<choiceName>>.
This choice's names must be in english and then translated in the yml translation files.
This provider should be Abstract and should be injected when needed.

E.g. on how should a provider look like:
```
class ThingProvider
{
    const A = 'choices.thing.a';
    const B = 'choices.thing.b';
    private static $thingChoices = array(
            self::A,
            self::B
            );
    public static function getTypeChoices()
    {
        return array_combine(self::$thingChoices, self::$thingChoices);
    }
}
```

These providers can be used e.g. within an Entity to assert values (@Assert\Choice) or a form to add choices.
ThingProvider::getTypeChoices()

## <a name="Dates"></a>Dates

All dates should be in `<<Day>>` `<<Month>>` `<<Year>>` format.

Localized dates: `{{ entity.createdAt | localizeddate('medium', 'none') }}`

reference: http://twig.sensiolabs.org/doc/extensions/intl.html

## <a name="DataFixtures"></a>Data Fixtures

One load data fixtures class should not load more than one entity.
A method "create…" should be implemented in order to create an entity.
e.g. createUser()
A class "DataFixture" should be created from which every loading fixtures responsible classes should extend.

## <a name="Forms"></a>Forms

### Dynamic Forms
http://symfony.com/doc/current/cookbook/form/dynamic_form_modification.html

### Change forms
Modify form based on submitted data:
Events:
`PRE_SET_DATA`
`POST_SUBMIT`

Create a closure to modify the form:
```
$formModifier = function (FormInterface $form, $thing) {
    if (null !== $thing && $thing != ThingProvider::A) {
         $form->add(...);
        …
    }
 };
 ```
 Call closure inside each event subscriber:
 ```
$builder->addEventListener(FormEvents::PRE_SET_DATA,
    function (FormEvent $event) use ($formModifier) {
        $formModifier($event->getForm(), $data->getThing());
});

$builder->get('thing')->addEventListener(
    FormEvents::POST_SUBMIT,
    function (FormEvent $event) use ($formModifier) {
        $formModifier($event->getForm()->getParent(), $thing);
 });
```

### Dependent Forms

Update the form using ajax
The trick to update the form using ajax, is just ask the form if the button was really pressed during the form submission.
```
if ($form->get('save')->isClicked() && $form->isValid()) {
```
### Form Events
http://symfony.com/doc/current/components/form/form_events.html

## <a name="Testing"></a>Testing

We will have blackbox and whitebox tests.

Blackbox tests may be using crawler and database.

Whitebox tests will be using behat+mink+something and will "always" use database.

Behat features folder will be placed in the project root dir.
Behat config file will be placed in the project root dir.
