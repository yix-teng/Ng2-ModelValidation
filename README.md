# Ng2-ModelValidation
Ability to use typescript annotation (same as es6 annotation) to angular2 models to include validation logic that can be used in model driven forms.


Our sample view model, decorated with annoations to help add validation logic.
```
class ViewModel {
	@required
	id: string;
	
	@range(1, 100)
	foo: number;
	
	@max-length(5)
	bar: string;
}
```


Our simple angular2 model driven form. 
```
@Component({
	template: `'
		<form [ngFormModel]="form" (ngSubmit)="onSubmit()">
        	<div class="row">
            	<label class="control-label" for="foo">Foo</label>
               	<input type="text" class="form-control" id="foo" ngControl="foo">
            </div>
        	<div class="row">
            	<label class="control-label" for="bar">Bar</label>
               	<input type="text" class="form-control" id="bar" ngControl="bar">
            </div>
            <button type="submit" class="btn">Submit</button>
       </form>
	'`
})
```
 

In the component, we need to inject the formbuilder via the construtor and include our module to get the validation logic from our model.

**Ng2ModelValidation.getValidation(vm)** will return the necessary information for the validation logic needed.

```
export class FooBarComponent {

	vm: ViewModel;

	form: ControlGroup;

	constructor(fb: FormBuilder) {
		this.form = fb.group(Ng2ModelValidation.getValidation(vm));
	}


	// ... rest of code here ...
	
}
```
