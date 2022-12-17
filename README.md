<h1 align="center">
  Fundamentals of Biomechanical Informatic
  <br>
</h1>

<img src="./assets/usage.png" alt="usage">
<p align="center">Access the WebApp <a href="https://biomec.netlify.app/" target="_blank">here</a>.</p>

<h2>
Atv. 3 • Task 1
</h2>

<h3>
JavaScript Code for Calculations
</h3>

```javascript
function calculateIntersectionPoint(){
  const divR = document.getElementById('result')
  const divG = document.getElementById('graph')

  var xA = window.document.getElementById("xA").value;
  var yA = window.document.getElementById("yA").value;
  var xB = window.document.getElementById("xB").value;
  var yB = window.document.getElementById("yB").value;
  var xPA = window.document.getElementById("xPA").value;
  var yPA = window.document.getElementById("yPA").value;
  var xPB = window.document.getElementById("xPB").value;
  var yPB = window.document.getElementById("yPB").value;

  if(xA == '' || yA == '' || xB == '' || yB == '' || xPA == '' || yPA == '' || xPB == '' || yPB == '') {
    alert('Preencha todos os campos.');
  }
  else {
    var xA = Number(xA)
    var yA = Number(yA);
    var xB = Number(xB);
    var yB = Number(yB);
    var xPA = Number(xPA);
    var yPA = Number(yPA);
    var xPB = Number(xPB);
    var yPB = Number(yPB);

    var A = [xA, yA];
    var B = [xB, yB];
    var PA = [xPA, yPA];
    var PB = [xPB, yPB];

    var slope_line_A = (A[1] - PA[1])/(A[0] - PA[0]);
    var slope_line_B = (B[1] - PB[1])/(B[0] - PB[0]);

    var intersec_X = (- (slope_line_B * B[0]) + B[1] + (slope_line_A * A[0]) - A[1])/(slope_line_A - slope_line_B);
    var intersec_Y = (slope_line_A * intersec_X) - (slope_line_A * A[0]) + A[1];

    var CA = {
        x: [A[0], PA[0]],
        y: [A[1], PA[1]],
        name: 'CA - PA',
        line: {
            color: '#885df5'
        }
    };

    var CB = {
        x: [B[0], PB[0]],
        y: [B[1], PB[1]],
        name: 'CB - PB',
        line: {
            color: '#00B37E'
        }
    };

    var data = [CA, CB];

    var layout = {
        width: 380,
        height: 300,
        xaxis: {
            title: "Eixo 1"
        },
        yaxis: {
            title: "Eixo 2"
        },
        title: 'Intersecção de retas "Câmera-Projeção"',
        showlegend: true,
        font: {
            family: 'Poppins'
        }
    };

    divR.innerHTML = `Ponto de intersecção (X, Y) = (${intersec_X.toFixed(3)}, ${intersec_Y.toFixed(3)})`;
    Plotly.newPlot('graph', data, layout);
  }    
}
```

<h2>
Atv. 5 • Task 3
</h2>

<h3>
JavaScript Code for Calculations
</h3>

```javascript

function calculateRotation() {
  function rotationMatrix(ang1, ang2, ang3, order) {
      var c1, c2, c3, matrix, s1, s2, s3;
      c1 = (Math.cos(ang1 * Math.PI / 180));
      s1 = (Math.sin(ang1 * Math.PI / 180));
      c2 = (Math.cos(ang2 * Math.PI / 180));
      s2 = (Math.sin(ang2 * Math.PI / 180));
      c3 = (Math.cos(ang3 * Math.PI / 180));
      s3 = (Math.sin(ang3 * Math.PI / 180));

      if(order === "xzx") {
          matrix = [[c2, -c3 * s2, s2 * s3], [c1 * s2, c1 * c2 * c3 - s1 * s3, -c3 * s1 - c1 * c2 * s3], [s1 * s2, c1 * s3 + c2 * c3 * s1, c1 * c3 - c2 * s1 * s3]];
      } else {
          if (order === "xyx") {
          matrix = [[c2, s2 * s3, c3 * s2], [s1 * s2, c1 * c3 - c2 * s1 * s3, -c1 * s3 - c2 * c3 * s1], [-c1 * s2, c3 * s1 + c1 * c2 * s3, c1 * c2 * c3 - s1 * s3]];
          } else {
          if (order === "yxy") {
              matrix = [[c1 * c3 - c2 * s1 * s3, s1 * s2, c1 * s3 + c2 * c3 * s1], [s2 * s3, c2, -c3 * s2], [-c3 * s1 - c1 * c2 * s3, c1 * s2, c1 * c2 * c3 - s1 * s3]];
          } else {
              if (order === "yzy") {
              matrix = [[c1 * c2 * c3 - s1 * s3, -c1 * s2, c3 * s1 + c1 * c2 * s3], [c3 * s2, c2, s2 * s3], [-c1 * s3 - c2 * c3 * s1, s1 * s2, c1 * c3 - c2 * s1 * s3]];
              } else {
              if (order === "zyz") {
                  matrix = [[c1 * c2 * c3 - s1 * s3, -c3 * s1 - c1 * c2 * s3, c1 * s2], [c1 * s3 + c2 * c3 * s1, c1 * c3 - c2 * s1 * s3, s1 * s2], [-c3 * s2, s2 * s3, c2]];
              } else {
                  if (order === "zxz") {
                  matrix = [[c1 * c3 - c2 * s1 * s3, -c1 * s3 - c2 * c3 * s1, s1 * s2], [c3 * s1 + c1 * c2 * s3, c1 * c2 * c3 - s1 * s3, -c1 * s2], [s2 * s3, c3 * s2, c2]];
                  } else {
                  if (order === "xyz") {
                      matrix = [[c2 * c3, -c2 * s3, s2], [c1 * s3 + c3 * s1 * s2, c1 * c3 - s1 * s2 * s3, -c2 * s1], [s1 * s3 - c1 * c3 * s2, c3 * s1 + c1 * s2 * s3, c1 * c2]];
                  } else {
                      if (order === "xzy") {
                      matrix = [[c2 * c3, -s2, c2 * s3], [s1 * s3 + c1 * c3 * s2, c1 * c2, c1 * s2 * s3 - c3 * s1], [c3 * s1 * s2 - c1 * s3, c2 * s1, c1 * c3 + s1 * s2 * s3]];
                      } else {
                      if (order === "yxz") {
                          matrix = [[c1 * c3 + s1 * s2 * s3, c3 * s1 * s2 - c1 * s3, c2 * s1], [c2 * s3, c2 * c3, -s2], [c1 * s2 * s3 - c3 * s1, c1 * c3 * s2 + s1 * s3, c1 * c2]];
                      } else {
                          if (order === "yzx") {
                          matrix = [[c1 * c2, s1 * s3 - c1 * c3 * s2, c3 * s1 + c1 * s2 * s3], [s2, c2 * c3, -c2 * s3], [-c2 * s1, c1 * s3 + c3 * s1 * s2, c1 * c3 - s1 * s2 * s3]];
                          } else {
                          if (order === "zyx") {
                              matrix = [[c1 * c2, c1 * s2 * s3 - c3 * s1, s1 * s3 + c1 * c3 * s2], [c2 * s1, c1 * c3 + s1 * s2 * s3, c3 * s1 * s2 - c1 * s3], [-s2, c2 * s3, c2 * c3]];
                          } else {
                              if (order === "zxy") {
                              matrix = [[c1 * c3 - s1 * s2 * s3, -c2 * s1, c1 * s3 + c3 * s1 * s2], [c3 * s1 + c1 * s2 * s3, c1 * c2, s1 * s3 - c1 * c3 * s2], [-c2 * s3, s2, c2 * c3]];
                              }
                          }
                          }
                      }
                      }
                  }
                  }
              }
              }
          }
          }
      }

      divR.innerHTML = `Elementos da Matriz de Rotação gerada: <br> <br> M11 = ${matrix[0][0].toFixed(3)} | M12 = ${matrix[0][1].toFixed(3)} | M13 = ${matrix[0][2].toFixed(3)}<br>M21 = ${matrix[1][0].toFixed(3)} | M22 = ${matrix[1][1].toFixed(3)} | M23 = ${matrix[1][2].toFixed(3)}<br>M31 = ${matrix[2][0].toFixed(3)} | M32 = ${matrix[2][1].toFixed(3)} | M33 = ${matrix[2][2].toFixed(3)}`;
  }

  const divR = document.getElementById('result')
  var ang1 = window.document.getElementById("ang1").value;
  var ang2 = window.document.getElementById("ang2").value;
  var ang3 = window.document.getElementById("ang3").value;
  var order = window.document.getElementById("order").value;

  var orders = ["xzx", "xyx", "yxy", "yzy", "zyz", "zxz", "xyz", "xzy", "yxz", "yzx", "zyx", "zxy"]

  if(ang1 == '' || ang2 == '' || ang3 == '' || order == '') {
      alert('Preencha todos os campos.');
  }
  else if(!orders.includes(order)) {
      alert('Selecione a ordem corretamente.<br>Possibilidades: xzx, xyx, yxy, yzy, zyz, zxz, xyz, xzy, yxz, yzx, zyx, zxy.');
  }
  else {
      var ang1 = Number(ang1);
      var ang2 = Number(ang2);
      var ang3 = Number(ang3);

      rotationMatrix(ang1, ang2, ang3, order)
  }
}

```