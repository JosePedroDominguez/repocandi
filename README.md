# repocandi
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { CandidateEntity } from 'ruta-hacia-CandidateEntity'; // Reemplaza con la ruta correcta

@Component({
  selector: 'app-candidate-form',
  templateUrl: './candidate-form.component.html',
  styleUrls: ['./candidate-form.component.css']
})
export class CandidateFormComponent implements OnInit {
  candidateForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.candidateForm = this.fb.group({
      name: ['', [Validators.required, Validators.maxLength(200)]],
      lastName: ['', [Validators.required, Validators.maxLength(200)]],
      email: ['', [Validators.required, Validators.maxLength(200)]],
      country: ['', Validators.maxLength(100)],
      address: ['', Validators.maxLength(100)],
      phoneNumber: ['', Validators.maxLength(15)],
      linkedIn: [Validators.maxLength(100)],
      idState: [null, Validators.required],
      idTrackPosition: [null, Validators.required],
    });
  }

  ngOnInit(): void {
  }

  onSubmit() {
    if (this.candidateForm.valid) {
      // Procesar el formulario y enviar los datos al servidor
      const formData = this.candidateForm.value;
      console.log(formData); // Puedes enviar esto al servidor
    }
  }
}

<section class="pt-5 section-admin-table">
  <form [formGroup]="candidateForm" (ngSubmit)="onSubmit()">
    <div class="d-flex gap-3 w-50 container-inputs">
      <label for="name">Name:</label>
      <input type="text" id="name" formControlName="name" class="form-control w-100">
    </div>
    <div class="d-flex gap-3 w-50 container-inputs">
      <label for="lastName">Last Name:</label>
      <input  class="form-control w-100" type="text" id="lastName" formControlName="lastName">
    </div>
    <div class="d-flex gap-3 w-50 container-inputs">
      <label for="email">Email:</label>
      <input  class="form-control w-100" type="text" id="email" formControlName="email">
    </div>
    <div class="d-flex gap-3 w-50 container-inputs">
      <label for="country">Country:</label>
      <input  class="form-control w-100" type="text" id="country" formControlName="country">
    </div>
    <div class="d-flex gap-3 w-50 container-inputs">
      <label for="address">Address:</label>
      <input  class="form-control w-100" type="text" id="address" formControlName="address">
    </div>
    <div class="d-flex gap-3 w-50 container-inputs">
      <label for="phoneNumber">Phone Number:</label>
      <input  class="form-control w-100" type="text" id="phoneNumber" formControlName="phoneNumber">
    </div>
    <div class="d-flex gap-3 w-50 container-inputs">
      <label for="linkedIn">LinkedIn:</label>
      <input  class="form-control w-100" type="text" id="linkedIn" formControlName="linkedIn">
    </div>
    <div class="d-flex gap-3 w-50 container-inputs">
      <label for="idState">State:</label>
      <select id="idState" formControlName="idState">
        <!-- Opciones de estados -->
      </select>
    </div>
    <div class="d-flex gap-3 w-50 container-inputs">
      <label for="idTrackPosition">Track Position:</label>
      <select id="idTrackPosition" formControlName="idTrackPosition">
        <!-- Opciones de posiciones -->
      </select>
    </div>
    <div>
      <button type="submit" [disabled]="!candidateForm.valid">Submit</button>
    </div>
  </form>
</section>
Asegúrate de reemplazar <!-- Opciones de estados --> y <!-- Opciones de posiciones --> con las opciones correspondientes para los campos idState e idTrackPosition. Puedes cargar estas opciones desde tu servidor o definirlas manualmente en el componente.

Paso 4: Estilizar el formulario
Puedes aplicar estilos CSS al formulario según tus necesidades en el archivo candidate-form.component.css.

Paso 5: Usar el componente en tu aplicación
Finalmente, utiliza el componente app-candidate-form en tu aplicación Angular donde desees mostrar el formulario.

Recuerda ajustar las rutas y las importaciones de los módulos según la estructura de tu proyecto y las dependencias que estés utilizando.








