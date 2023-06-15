# TAREA1_CAMARA

APLICACION PARA TOMAR FOTO Y GUARDAR EN ALMACENAMIENTO INTERNO
por: Bryan Chicaiza

para la realizacion de la presente aplicacion de tomar fotos con la camara se hizo el uso principalmente de un imageview e image button 
programando en el activitymain las distintas funciones, declaracion de variables, y creacion de los distintos metodos, tanto como el imagebutton 
para que pueda tomar la foto, hacer que esa foto se muestre en el imageview y dar los respectivos permisos en el androidmanifest.xml para que estas fotos puedan ser 
guardadas en el dispositivo

# CODIFICACION EN EL ACTIVITYMAIN.JAVA
public class MainActivity extends AppCompatActivity {
    ImageView imagen;
    ImageButton boton;
    String rutaImagen;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        imagen = findViewById(R.id.imageView);
        boton = findViewById(R.id.imageButton);

        boton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                abrircamara();
            }
        });
    }
    //metodo para habilitar la camara
    private void abrircamara(){
        Intent intent= new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
        File imagenarchivo=null;
        try {
            imagenarchivo=crearimagen();
        }catch(IOException ex){
            Log.e("error", ex.toString());
             }
        if (imagenarchivo!=null){
            Uri fotouri= FileProvider.getUriForFile(this, "com.example.tomarfoto.fileProvider", imagenarchivo);
            intent.putExtra(MediaStore.EXTRA_OUTPUT, fotouri);
            startActivityForResult(intent, 1);
        }

    }

    //metodo para visualizar la imagen capturada en el imageview

    protected void onActivityResult(int requestCode, int resultCode, Intent data){
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == 1 && resultCode == RESULT_OK) {
            Bitmap imageBitmap = BitmapFactory.decodeFile(rutaImagen);
            imagen.setImageBitmap(imageBitmap);
        }
    }

    //metodo para crear el archivo temporal de la foto que sera de tipo jpg

    private File crearimagen()throws IOException{
        String nombreimagen="foto_ ";
        File directorio=getExternalFilesDir(Environment.DIRECTORY_PICTURES);
        File imagen2=File.createTempFile(nombreimagen, ".jpg", directorio);
        rutaImagen=imagen2.getAbsolutePath();
        return imagen2;
    }
    
    }


![image](https://github.com/JoseCaiza/AppMovil202350/assets/133244305/0c3f5a38-8c2a-4d62-9a89-c7f8bac8ae4b)

para una mejor visualizacion de la practica se la realizo en el celular personal para  poder encontrar las imagenes de manera mas rapida

# INTERFAZ DE APLICAION

![WhatsApp Image 2023-06-14 at 8 36 23 PM (1)](https://github.com/JoseCaiza/AppMovil202350/assets/133244305/1a6cf0a1-b2f7-4d96-acf3-3ccf30955d0b)

# LUGAR EN EL QUE SE GUARDAN LAS IMAGENES

![WhatsApp Image 2023-06-14 at 8 36 23 PM](https://github.com/JoseCaiza/AppMovil202350/assets/133244305/81b52cde-038a-4773-841c-f56976993c8b)
