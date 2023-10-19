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
  <form [formGroup]="candidateForm" (ngSubmit)="onSubmit()" class="container">
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="name" class="form-label">Name:</label>
        <input type="text" id="name" formControlName="name" class="form-control">
      </div>
      <div class="col-md-6">
        <label for="lastName" class="form-label">Last Name:</label>
        <input type="text" id="lastName" formControlName="lastName" class="form-control">
      </div>
    </div>
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="email" class="form-label">Email:</label>
        <input type="text" id="email" formControlName="email" class="form-control">
      </div>
      <div class="col-md-6">
        <label for="country" class="form-label">Country:</label>
        <input type="text" id="country" formControlName="country" class="form-control">
      </div>
    </div>
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="address" class="form-label">Address:</label>
        <input type="text" id="address" formControlName="address" class="form-control">
      </div>
      <div class="col-md-6">
        <label for="phoneNumber" class="form-label">Phone Number:</label>
        <input type="text" id="phoneNumber" formControlName="phoneNumber" class="form-control">
      </div>
    </div>
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="linkedIn" class="form-label">LinkedIn:</label>
        <input type="text" id="linkedIn" formControlName="linkedIn" class="form-control">
      </div>
      <div class="col-md-6">
        <label for="idState" class="form-label">State:</label>
        <select id="idState" formControlName="idState" class="form-select">
          <!-- Opciones de estados -->
        </select>
      </div>
    </div>
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="idTrackPosition" class="form-label">Track Position:</label>
        <select id="idTrackPosition" formControlName="idTrackPosition" class="form-select">
          <!-- Opciones de posiciones -->
        </select>
      </div>
    </div>
    <div class="text-center">
      <button type="submit" [disabled]="!candidateForm.valid" class="btn btn-primary">Submit</button>
    </div>
  </form>
</section>

Asegúrate de reemplazar <!-- Opciones de estados --> y <!-- Opciones de posiciones --> con las opciones correspondientes para los campos idState e idTrackPosition. Puedes cargar estas opciones desde tu servidor o definirlas manualmente en el componente.

Paso 4: Estilizar el formulario
Puedes aplicar estilos CSS al formulario según tus necesidades en el archivo candidate-form.component.css.

Paso 5: Usar el componente en tu aplicación
Finalmente, utiliza el componente app-candidate-form en tu aplicación Angular donde desees mostrar el formulario.

Recuerda ajustar las rutas y las importaciones de los módulos según la estructura de tu proyecto y las dependencias que estés utilizando.








