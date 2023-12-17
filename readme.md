# Spring PetClinic Sample Application

This project is used as part of the Java Department Meeting #3 Workshop!
The workshop showcases IntelliJ capabilities & aims at improving this tool's understanding through a set of tiny actions!

## Getting started
- [ ] Task: Use IntelliJ to create a new project based on this remove repository.
- [ ] How to: 
    - [ ] Open up IntelliJ
    - [ ] Under File choose New > Project from Version Control
    - [ ] Under URL paste in https://github.com/lelexy100/spring-petclinic.git
    - [ ] Under directory, choose a path where the project should be created
    - Note that this method is helpful when the sources are not already present on your machine. If you've already downloaded the sources, you can make a new IntelliJ project by using File > New > Project from existing sources
    - [ ] Clone & import as a maven project.
    - [ ] Reload the Maven project to download dependencies by finding the Maven window on the right hand side of the screen & clicking the reload button.

## Context
Welcome to PetClinic! This app can be used to keep track of doctors, pets, owners and appointments that pets have in the pet clinic!

Today we'll be exploring some IntelliJ features while playing with this app's code!

Note that while you will not need to launch the app for this workshop, you can do it, given you have JDK17 on your machine. You can find the class PetClinicApplication, launch it as a SpringBoot app and consult the app at http://localhost:8080 .

## Let's go!
As you're probably not familliar with this project, this guide will guide you towards finding different things we'd like to change, and tell you how to do it. If you already know how to do something, feel free to ignore the "How to:" section.

* Task: Use Go to File to open up `PetController.java`
  * How to: 
    * Open the Go to File window by using the hotkey (IntelliJ: Ctrl+Shift+N, Eclipse: Ctrl+Shift+R)
    * Type / Paste in `PetController.java`
    * Double click the file in the list
  * Info: The Go to File shortcut is very valuable in finding your way around a project. The tool allows for many parameters that can help in fine-graining your search for files.


* Task: Locate the method `processCreationForm` in `PetController.java` and extract the validation into a new method
  * How to:
    * Use the search function (Ctrl+F) to locate `processCreationForm` inside `PetController.java`
    * Make a selection with your cursor around the lines containing validation (lines 98 to 105)
    * Right click on this selection, choose Refactor > Extract method... Alternatively, you can use the hotkey (IJ: Ctrl+Alt+M, E: Alt+Shift+M)
    * Type / paste in the new name for this new function: `validateFormCreation`
  * Info: Extracting methods is very common when developing, getting used to the hotkey will save you a lot of time!
  * New task: Locate the method `processUpdateForm` in `PetController.java` and extract the validation into a new method `validateFormUpdate`.


* Task: Locate the method `validateBirthDate` in `PetValidator.java` and inline + remove it.
  * How to:
    * Use Go to File to locate the file `PetValidator` and Search to locate `validateBirthDate` inside the file. 
    * Right click on the method name (`validateBirthDate`) and choose Refactor > Inline method... Alternatively you may use the hotkey (IJ: Ctrl+Alt+N, E: Alt+Shift+I)
    * In the popup, choose to inline and remove the function, then click Refactor.
  * Info: Inlining methods is the reverse operation to extracting methods and can help easily get rid of some unneeded abstractions. 
  * New task: Locate the method `validatePetType` in `PetValidator.java` and inline + remove it.


* Task: Locate the method at line 122, column 25 in OwnerController and rename it to `findByLastname`
* How to:
  * Use Go to File to locate the file `OwnerController`
  * Use the Go to Line:Column column through the hotkey (IJ: Ctrl+G, E: Ctrl+L) and type in 122:25
  * Right click the method name, Refactor > Rename... or use the hotkey (IJ: Shift+F6, E: Alt+Shift+R) and type / paste `findByLastname`.
* New task: Locate the method at line line 113, column 20 and rename it to `addPaginationToModel`.


* Task: Extract a local variable named `totalPages` in the new `addPaginationToModel` method.
* How to:
  * In the `OwnerController` file, in the newly renamed method `addPaginationToModel`, identify the expression `paginated.getTotalPages()`
  * Highlight the expression, right click it and Refactor > Introduce variable... or use the hotkey (IJ: Ctrl+Alt+V, E: Alt+Shift+L)
  * Set the name to `totalPages` if not already suggested by IJ.
* New task: Extract a local variable named `totalItems` in the new `addPaginationToModel` method.


* Task: Extract the constant `pageSize` from `findByLastname` in `OwnerController`
* How to: 
  * In the `OwnerController` file, find the `findByLastname` method and locate the expression: `int pageSize = 5;`
  * Highlight the expression, right click it and Refactor > Introduce constant... or use the hotkey (Ctrl+Alt+C)
  * Name the new constant `PAGE_SIZE` and validate that it was properly used in the creation of the `Pageable`, one line lower.
* New task: Extract the constant `pageSize` from `findPaginated` in `VetController`.


* Task: Introduce a parameter from the `Pageable` object and remove useless parameters from the method `findByLastname` in `OwnerController`
* How to:
  * In the `OwnerController` file, find the `findByLastname` method and locate the expression: `Pageable pageable = PageRequest.of(page - 1, PAGE_SIZE);`
  * Highlight the expression, right click it and Refactor > Introduce parameter... or use the hotkey (Ctrl+Alt+P)
  * Before confirming the new name for the parameter, check out the method signature: a new parameter is added in, `pageable` and a parameter that was previously received, `name` is strikedthrough.
  * Confirm the new parameter `pageable` and notice that `name` has disappeared from the method signature.
* Info: Because `name` is only used in the creation of `pageable` and `pageable` is transformed into a parameter, `name` is no longer needed, and IntelliJ recognizes that it should be removed.
* New task: Introduce the parameters `owners` (from the local variable `listOwners`), `totalPages` and `totalItems` in the method `addPaginationToModel` of the file `OwnerController`.


* Task: Reorder the parameters of the method `addPaginationModel` in the class `VetController` so that `page` is last.
* How to: 
  * Find the file `VetController` and the method `addPaginationModel`
  * Right click on the `addPaginationModel` method name and Refactor > Change signature... or use the hotkey (IJ: Ctrl+F6, E: Alt+Shift+C)
  * In the list of parameters, click the first one (`page`)
  * Click on the arrow pointing down twice, so that `page` is now the last parameter.
  * Click Refactor and notice how the parameter position changed in both the method signature and in places calling the method (right above the method declaration.)
* Info: There are many other great features you can accomplish with Change signature..., feel free to explore some more after the workshop!
* New task: Reorder the parameters of the method `showVetList` in the class `VetController` so that `page` is last. What do you notice about the annotation?


* Task: Remove the useless parameter `model` of the function `triggerException` in `CrashController`
* How to:
  * Find the file `CrashController` and the method `triggerException`
  * Notice how the parameter `model` is grayed out since it's unused in the method body.
  * Right click the parameter and Refactor > Change signature... or use the hotkey (IJ: Ctrl+F6, E: Alt+Shift+C)
  * Click the parameter in the list of parameters and then the `-` symbol
  * Click Refactor and then Continue when asked for an unsafe delete.
  * Notice how the parameter was removed in both the method implementation and the test in `CrashControllerTests.java`


* Task: Find the method `getId` in the class `NamedEntity` using `File structure`
* How to:
  * Find the class `NamedEntity` and notice how it extends the class `BaseEntity`
  * Open the `File structure` window by using the hotkey (IJ: Ctrl+F12, E: Ctrl+O)
  * Type `getId` and notice how the method is found in the list of methods even though this method does not belong to the class NamedEntity
  * Notice how the parameter `Inherited members` has turned on.
* Info: The file structure search is one of the most powerful search mechanisms in IntelliJ - in complex inheritance hierarchies it will simplify navigating to the right superclass, in XML/JSON files it allows going straight to certain nodes, etc.


* Task: Find all subclasses of `BaseEntity` using the Type Hierarchy
* How to:
  * Find the class `BaseEntity`, click its name and open the Type Hierarchy by using the hotkey (IJ: Ctrl+H, E: F4)
  * Notice the new window opens and shows all the classes that extend the `BaseEntity`
  * Uncollapse the collapsed classes in the window and notice that even anonymous implementations are shown!


* Task: Create a new class called `PetCreationValidator`, declare it as a `private final field` of `PetController` and inject it in its constructor.
* How to:
  * In the Project View (Alt+1) Go to the package that contains the `PetController` class and right click its parent folder then create a new class `PetCreationValidator` next to `PetController`.
  * Annotate the newly created class with `@Component`
  * In the `PetController` class, create a new `private final PetCreationValidator petCreationValidator;`
  * Notice an error is shown because the validator is declared as final but never initialized.
  * Use the Show Quick Fixes command, hotkey (Alt+Enter) and choose Add constructor parameter.
  * Notice how the additional parameter is added to the constructor and the validator is now injected.


* Task: Move the method `validateFormCreation` into the new `PetCreationValidator` and rename it to `validate`
* How to:
  * In the `PetController` class, find the method `validateFormCreation` and make sure the method is NOT static. If it is, remove the static keyword.
  * Right click the method name and choose Refactor > Move Instance Method... or use the hotkey (IJ: F6, E: Alt+Shift+V)
  * A new window showing the possible instances where the method can be moved will show up. Choose `PetCreationValidator`.
  * Ensure the new visibility is set to `public` on the right hand side of the window, then click Refactor.
  * Go to `PetCreationValidator` and notice that the method has been moved.
  * Rename the method `validateFormCreation` into `validate`.
* Info: when moving the method to a different instance, the window allows setting up different visibilities for the newly moved method. Most notably, `Escalate` will set the visibility to the most restrictive one that still allows using the method from the new class parent. In our case, we went for `public` since we'll move this class to a different package eventually.


* Task: Extract the method `validateFormUpdate` into a superclass of `PetController`
* How to:
  * In the `PetController` class, find the method `validateFormUpdate` and make sure the method is NOT static. if it is, remove the static keyword.
  * Right click the `PetController` class name and choose Refactor > Extract Superclass...
  * In the new window, in the `Superclass name` field, type / paste in `PetControllerTemp`.
  * In the list of methods implemented in the class, choose the method `validateFormUpdate` and click Refactor.
  * In the window asking to Find and replace usages, click `No`. If a window appears asking to add the file to VCS, you can click either `yes` or `no`.
  * In the `PetController` class, notice how the class now extends our newly created class.
  * In the `PetControllerTemp` class, notice how the method has been moved. If the method is not `public`, make it `public` since we'll need that in a future step.
* Info: extracting a superclass can be very useful on its own whenever we need to create a new abstraction but even more so when coupled with replacing inheritance with composition.


* Task: Replace `PetController`'s inheritance with composition and rename the new member to `PetUpdateValidator`
* How to:
  * In the `PetController` class, right click on the class name and choose Refactor > Replace inheritance with delegation...
  * In the new refactor window, choose the name of the field for the new resource as `petControllerTemp` and make sure that there are no delegate members selected. Having them selected introduces an additional wrapper method that we don't need.
  * Click Refactor and notice how now the inheritance has disappeared, and in its place, we have a new field.
  * The new field is created statically which we don't want, we'll inject it through the constructor.
  * In the `PetControllerTemp` class, annotate the class with `@Component`.
  * In the `PetController` class, you may now remove the instantiation of the `PetControllerTemp` by replacing:
```java
private final PetControllerTemp petControllerTemp = new PetControllerTemp();
```
with
```java
private final PetControllerTemp petControllerTemp;
```
* 
  * You will now have an error that you can fix by injecting this new dependency in the constructor, as done in a previous example.
  * Rename the class `PetControllerTemp` into `PetUpdateValidator` by going in the class `PetControllerTemp`, right clicking the class' name and choosing Refactor > Rename...
  * In the refacto window, click `Select All` to choose to replace all members having the old name, with the new one. Click Ok.
  * In the Rename confirmation window, find the category `[In Strings, Comments, and Text]`, uncolapse it and right click > Exclude the file `readme.md` from the replace - otherwise you will break this readme :).
  * Click `Do Refactor` and notice how now the class is named PetUpdateValidator, the field where the validator is references is also renamed.
  * Finally, rename the method `validateFormUpdate` from `PetUpdateValidator` into `validate`.


* Task: Make a new package for validators and move them there.
* How to:
  * In the Project View (Alt+1), create a new package in the same package that contains `PetController`, by right clicking the `owner` folder and choosing New > Package
  * The full package name should be `org.springframework.samples.petclinic.owner.validator` which is just adding `validator` at the end of the previous package.
  * In the Project View, choose both newly created validators, by clicking `PetUpdateValidator` and then holding down Ctrl before clicking `PetCreationValidator`.
  * Having the 2 selected, right click one of them and choose Refactor > Move class...
  * In the new window, paste in the newly created package `org.springframework.samples.petclinic.owner.validator` and click Refactor.
  * If you get a new window showing conflicts, you probably haven't made one of the 2 `validate` methods public in one of the previous steps.


* Task: That's all! Let me know your thoughts on this workshop and fill in the feedback form I'll be sending later today / tomorrow :D

