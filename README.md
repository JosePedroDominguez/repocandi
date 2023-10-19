control => {    return hasValidLength(control.value) && control.value.length > maxLength ? {      'maxlength': {        'requiredLength': maxLength,        'actualLength': control.value.length      }    } : null;  }



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
    <div class="border-bottom container-h1 m-auto mb-5">
      <h1 class="mb-4 fs-1 title fw-bold">Create Candidate</h1>
    </div>
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="name" class="form-label">Name:</label>
        <input type="text" id="name" formControlName="name" class="form-control" required maxlength="200">
        <div *ngIf="candidateForm.get('name')?.hasError('maxlength')" class="text-danger">Name cannot exceed 200 characters.</div>
      </div>
      <div class="col-md-6">
        <label for="lastName" class="form-label">Last Name:</label>
        <input type="text" id="lastName" formControlName="lastName" class="form-control" required maxlength="200">
        <div *ngIf="candidateForm.get('lastName')?.hasError('maxlength')" class="text-danger">Last Name cannot exceed 200 characters.</div>
      </div>
    </div>
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="email" class="form-label">Email:</label>
        <input type="text" id="email" formControlName="email" class="form-control" required maxlength="200">
        <div *ngIf="candidateForm.get('email')?.hasError('maxlength')" class="text-danger">Email cannot exceed 200 characters.</div>
      </div>
      <div class="col-md-6">
        <label for="country" class="form-label">Country:</label>
        <input type="text" id="country" formControlName="country" class="form-control" maxlength="100">
      </div>
    </div>
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="address" class="form-label">Address:</label>
        <input type="text" id="address" formControlName="address" class="form-control" maxlength="100">
      </div>
      <div class="col-md-6">
        <label for="phoneNumber" class="form-label">Phone Number:</label>
        <input type="text" id="phoneNumber" formControlName="phoneNumber" class="form-control" maxlength="15">
      </div>
    </div>
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="linkedIn" class="form-label">LinkedIn:</label>
        <input type="text" id="linkedIn" formControlName="linkedIn" class="form-control" maxlength="100">
      </div>
      <div class="col-md-6">
        <label for="idState" class="form-label">State:</label>
        <select id="idState" formControlName="idState" class="form-select" required>
          <option value="" disabled>Select a state</option>
          <option>  </option>
        </select>
      </div>
    </div>
    <div class="row mb-3">
      <div class="col-md-6">
        <label for="idTrackPosition" class="form-label">Track Position:</label>
        <select id="idTrackPosition" formControlName="idTrackPosition" class="form-select" required>
          <option value="" disabled>Select a track position</option>
          <option *ngFor="let track of availableTrackPositions" [value]="track.id">{{track.trackPosition}}</option>
        </select>
      </div>
      <div class="col-md-6">
        <label for="idSkill" class="form-label">Skills:</label>
        <select id="idSkill" formControlName="idSkill" class="form-select" required>
          <option value="" disabled>Select a skill</option>
          <option *ngFor="let skill of availableSkills" [value]="skill.id">{{skill.skill}}</option>
        </select>
      </div>
    </div>
    <div class="d-flex gap-3">
      <button class="btn btn-outline-success" type="submit" [disabled]="!candidateForm.valid">
        Create <span class="iconify" data-icon="ic:twotone-check-box"></span>
      </button>
      <button class="btn btn-outline-danger me-3" type="button" (click)="CleanForm()">
        Cancel <span class="iconify" data-icon="ic:twotone-cancel"></span>
      </button>
    </div>
  </form>
</section>


Asegúrate de reemplazar <!-- Opciones de estados --> y <!-- Opciones de posiciones --> con las opciones correspondientes para los campos idState e idTrackPosition. Puedes cargar estas opciones desde tu servidor o definirlas manualmente en el componente.

Paso 4: Estilizar el formulario
Puedes aplicar estilos CSS al formulario según tus necesidades en el archivo candidate-form.component.css.

Paso 5: Usar el componente en tu aplicación
Finalmente, utiliza el componente app-candidate-form en tu aplicación Angular donde desees mostrar el formulario.

Recuerda ajustar las rutas y las importaciones de los módulos según la estructura de tu proyecto y las dependencias que estés utilizando.
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

import { environment } from 'src/environment/environment';
import { ResponseDto } from '../models/response.dto';

import {
  SkillInsertModel,
  SkillUpdateModel,
} from '../models/skill.model';

@Injectable({
  providedIn: 'root'
})

export class SkillService {
  private urlApi: string = `${environment.apiCandidates}${environment.serviceSkill}`;
  constructor(private http: HttpClient) {}

  getAll(): Observable<ResponseDto> {
    return this.http.get<ResponseDto>(`${this.urlApi}GetAll`);
  }

  insert(model: SkillInsertModel): Observable<ResponseDto> {
    return this.http.post<ResponseDto>(`${this.urlApi}Insert`, model);
  }

  update(model: SkillUpdateModel): Observable<ResponseDto> {
    return this.http.put<ResponseDto>(`${this.urlApi}Update`, model);
  }

  delete(id: number): Observable<ResponseDto> {
    return this.http.delete<ResponseDto>(`${this.urlApi}Delete/?id=${id}`);
  }
}
import { Component, OnInit, ViewChild } from '@angular/core';
import { MatTableDataSource } from '@angular/material/table';
import { MatPaginator } from '@angular/material/paginator';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

import { SkillService } from 'src/app/services/skill.service';
import { SkillInsertModel, SkillUpdateModel } from 'src/app/models/skill.model';
import { ResponseDto } from 'src/app/models/response.dto';

import Swal from 'sweetalert2';

@Component({
  selector: 'app-skill',
  templateUrl: './skill.component.html',
  styleUrls: ['./skill.component.css']
})
export class SkillComponent implements OnInit {
  form: FormGroup;
  displayedColumns: string[] = ['Skill', 'delete', 'edit'];
  dataSource = new MatTableDataSource<SkillUpdateModel>([]);
  editingSkill: SkillUpdateModel = { id: 0, skill: '' };
  creatingSkill: SkillInsertModel = { skill: '' };
  isCreating: boolean = false;
  newSkill = { Id: 0, Skill: '', isEditing: true, isCreating: true };

  @ViewChild(MatPaginator) paginator!: MatPaginator;

  constructor(private skillService: SkillService, private fb: FormBuilder) {
    this.form = this.fb.group({
      Skill: [
        '' || null,
        [Validators.required, Validators.maxLength(100)]
      ],
    });
  }

  ngOnInit() {
    this.dataSource.paginator = this.paginator;
    this.loadSkills();
  }

  loadSkills() {
    this.skillService.getAll().subscribe(
      (res) => {
        this.dataSource.data = res.result as SkillUpdateModel[];
      }
    );
  }

  editSkill(skill: SkillUpdateModel) {
    this.newSkill.isEditing = true;
    this.editingSkill = skill;
  }

  cancelEdit(skill: SkillUpdateModel) {
    this.editingSkill = { id: 0, skill: '' };
    this.newSkill.isEditing = false;
  }

  saveSkillEdited() {
    if (this.editingSkill) {
      if (this.form.get('Skill')?.hasError('maxlength')) {
        Swal.fire('Error!', 'Skill cannot exceed 100 characters.', 'error');
        return;
      }

      if (this.editingSkill) {
        this.skillService.update(this.editingSkill).subscribe(
          (response: ResponseDto) => {
            Swal.fire('Success!', 'Skill updated successfully', 'success');
            this.loadSkills();
            this.editingSkill = { id: 0, skill: '' };
          },
          (error) => {
            Swal.fire('Error!', 'Failed to update skill.');
            setTimeout(() => {
              window.location.reload();
            }, 5000);
          }
        );
      }
    }
  }

  startCreating() {
    this.isCreating = true;
  }

  cancelCreating() {
    this.isCreating = false;
    this.newSkill = { Id: 0, Skill: '', isEditing: true, isCreating: true };
  }

  saveCreatingSkill() {
    if (this.editingSkill) {
      if (this.form.get('Skill')?.hasError('maxlength')) {
        Swal.fire('Error!', 'Skill cannot exceed 100 characters.', 'error');
        return;
      }

      this.creatingSkill.skill = this.form.get('Skill')?.value;

      this.skillService.insert(this.creatingSkill).subscribe(
        (response: ResponseDto) => {
          Swal.fire('Success!', 'Skill created successfully', 'success');
          this.loadSkills();
          this.isCreating = false;
          this.newSkill = { Id: 0, Skill: '', isEditing: true, isCreating: true };
        },
        (error) => {
          console.error(error);
          Swal.fire('Error!', 'Failed to create Skill. Error: ' + error.error.ExceptionMessage, 'error');
          setTimeout(() => {
            window.location.reload();
          }, 2000);
        }
      );
    }
  }


  deleteSkill(id: number) {
    Swal.fire({
      title: 'Are you sure?',
      text: "You won't be able to revert this operation!",
      icon: 'warning',
      showCancelButton: true,
      confirmButtonColor: '#3085d6',
      cancelButtonColor: '#d33',
      cancelButtonText: 'Cancel',
      confirmButtonText: 'Yes, Delete!',
    }).then((result) => {
      if (result.isConfirmed) {
        this.skillService.delete(id).subscribe(
          (response: ResponseDto) => {
            Swal.fire(
              'Deleted!',
              'The Skill has been deleted.',
              'success'
            ).then(() => {
              this.loadSkills();
            });
          },
          (error) => {
            console.error(error);
            Swal.fire('Error!', 'Failed to delete Skill.');
            setTimeout(() => {
              window.location.reload();
            }, 2000);
          }
        );
      }
    });
  }
}
export interface SkillInsertModel {
    skill: string;
}

export interface SkillUpdateModel {
    skill: string;
    id: number;
}







