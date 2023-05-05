# Update-API-Connection
===========Api connection Step=========

Step 1: Ng new Api //Project Create

step 2: ng g c Data //Component Genrate

step 3: ng g s APi_Service //Service Create
-------------------------------------------------------------------------------------
1)	open app.module.ts file

			import { HttpClientModule } from '@angular/common/http';

		imports{
			HttpClientModule
		}
------------------------------------------------------------------------------------
2) 	open api.service.ts File

 	import{ HttpClient} from '@angular/common/http';

 	 export class APIService {
	  constructor(private http:HttpClient) { }
	  Data(){
	    return this.http.get('Fake API Link');
  	 }
	   userDataSendBackend(data:any){
	    return this.http.post('http://localhost:8000/insert',data);
	  }

	  deletef(idu:any){
	    let obj={id:idu};
	    return this.http.post('http://localhost:8000/delete',obj);
	  }
	  editUserDate(obj:any,id:any){
	     obj.id=id;
	     return this.http.post('http://localhost:8000/edit',obj);
	  }
	  singleUserData(idu:any){
	    let obj={id:idu};
	    return this.http.post('http://localhost:8000/onedata',obj);
	  }
	}
 ------------------------------------------------------------------------------------

3) 	open data.component.ts

 	 export class DataComponent {
	  constructor(private ser:ApiService, private fb:FormBuilder){}
	  DATA:any;
	  formData: any;
	  ngOnInit():void{
	    this.ser.data().subscribe((res)=>{
	      this.DATA=res;
	    })
	    this.formData=this.fb.group({
	      username:[''],
	      password:['']
	    })
	  }

	  submitData(){
	    this.ser.userDataSendBackend(this.formData.value).subscribe((res: any)=>{
	    console.log(res);    
	    })
	    console.log(this.formData.value);

	  }
	  del(id:any){
	    this.ser.deletef(id).subscribe((res)=>{
	      console.log(res);

	    })
	  }

	  editdata(id:any){
	    this.ser.editUserDate(this.formData.value,id).subscribe((res)=>{
	      console.log(res);

	    })
	  }
	  singleuserdata:any;
	  onedata(id:any){
	    this.ser.singleUserData(id).subscribe((res)=>{
	      this.singleuserdata=res;
	    })
	  }
	}

 ------------------------------------------------------------------------------------

 open data.component.html

 		{{DATA|json}}  //print Pipe Data

 ------------------------------------------------------------------------------------

