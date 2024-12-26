# Tic_Tac_Toe_Game


-----------This is the java code of Game--------------
package com.newproj.tictactoe;

import android.os.Bundle;
import android.view.View;
import android.widget.ImageView;
import android.widget.TextView;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class MainActivity extends AppCompatActivity {
    //Player represntions

    //0 -> X
    //1 -> o

    int activeplayer=0;

    int [] gamestate={2,2,2,2,2,2,2,2,2};

        //sates
        //0 -> X
        //1 -> o
        //2 -> null

    int[][]winigpostions={{0,1,2},{3,4,5},{6,7,8},
                          {0,3,6},{1,4,7},{2,5,8},
                          {0,4,8},{2,4,6}};
      boolean gameactive = true;

    public void playerTap(View view){

             ImageView img =(ImageView) view;
             int tappedimage =Integer.parseInt(img.getTag().toString());

             if(!gameactive){
                 gamereset(view);
             }

             if(gamestate[tappedimage]==2){
                gamestate[tappedimage]=activeplayer;
                img.setTranslationY(-1000f);

                if(activeplayer==0){
                    img.setImageResource(R.drawable.x);
                    activeplayer=1;
                    TextView status =findViewById(R.id.status);
                    status.setText("O's Turn-Tap To Play");
                }else{
                    img.setImageResource(R.drawable.o);
                    activeplayer=0;
                    TextView status =findViewById(R.id.status);
                    status.setText("x's Turn-Tap To Play");
                }
                img.animate().translationYBy(1000f).setDuration(300);
             }

              //check anyone has won
              for(int []winigpostion:winigpostions){
                  if(gamestate[winigpostion[0]]==gamestate[winigpostion[1]] &&
                          gamestate[winigpostion[1]]==gamestate[winigpostion[2]]&&
                          gamestate[winigpostion[0]]!=2 ){

//                      check who is win x or o

                      String winner;
                       gameactive=false;


                      if(gamestate[winigpostion[0]]==0){
                        winner="X Has Won ";
                      }
                      else {
                       winner="O Has Won";
                      }

                      



                      TextView status =findViewById(R.id.status);
                      status.setText(winner);

                  }
              }

          }
    public void gamereset(View view){
        gameactive=true;
        activeplayer=0;

        for(int i=0;i<gamestate.length;i++){

            gamestate[i]=2;

            ((ImageView)findViewById(R.id.imageView1)).setImageResource(0);
            ((ImageView)findViewById(R.id.imageView2)).setImageResource(0);
            ((ImageView)findViewById(R.id.imageView3)).setImageResource(0);
            ((ImageView)findViewById(R.id.imageView4)).setImageResource(0);
            ((ImageView)findViewById(R.id.imageView5)).setImageResource(0);
            ((ImageView)findViewById(R.id.imageView6)).setImageResource(0);
            ((ImageView)findViewById(R.id.imageView7)).setImageResource(0);
            ((ImageView)findViewById(R.id.imageView8)).setImageResource(0);
            ((ImageView)findViewById(R.id.imageView9)).setImageResource(0);


            TextView status =findViewById(R.id.status);
            status.setText("x's Turn-Tap To Play");

        }
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
    }
}
