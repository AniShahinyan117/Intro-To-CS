# Intro-To-CS
// Problem 1
function calculateDistance(p1, p2) {
    n = p1.length;
    let d = 0;
    for (let i = 0; i < n; i++) {
        d += (p1[i] - p2[i]) ** 2;
    }
    return Math.sqrt(d);
}
function p1() {
    console.log(calculateDistance([5, 6, 8], [14, 13, 6]));
}
p1();

// Problem 2

function determineMatrixType(m) {
    for (let i = 1; i < m.length; i++) {
        if (m[i].length != m[0].length)
            return 0;
    }
    if (m[0].length == m.length)
        return 2;
    if (m[0].length == 1)
        return -1;
    else return 1;
}
let matrix1 = [
    [1, 2, 3],
    [2, 3, 4],
    [3, 4, 5]
];
let matrix2 = [
    [1, 2, 3, 4],
    [1, 2, 3, 4]
];
let matrix3 = [
    [1, 2, 3],
    [1, 2, 3, 4, 5]
];
let matrix4 = "words";
function p2() {
    console.log(determineMatrixType(matrix1));
    console.log(determineMatrixType(matrix2));
    console.log(determineMatrixType(matrix3));
    console.log(determineMatrixType(matrix4));
}
p2();

// Problem 3

function transposeMatrix(m) {
    let result = new Array(m[0].length);
    for (let i = 0; i < m[0].length; i++) {
        result[i] = new Array(m.length);
        for (let j = 0; j < m.length; j++) {
            result[i][j] = m[j][i];
        }
    }
    return result;
}
matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
]
function p3() {
    console.log(transposeMatrix(matrix));
}
p3();

//Problem 4

const spiralMatrix = n => {
    let fill = (n * n) - 1;
    let m = [];

    for (let i = 0; i < n; i++) {
        m[i] = [];
        for (let j = 0; j < n; j++) {
            m[i][j] = 0;
        }
    }

    const moveDown = (i, j) => {
        if (fill > 0) {

            if ((i + 1 <= n - 1) && (m[i + 1][j] == 0)) {
                m[i + 1][j] = fill;
                fill--;
                moveDown(i + 1, j);
            } else moveRight(i, j);
        }
    }

    const moveUp = (i, j) => {
        if (fill > 0) {

            if ((i - 1 >= 0) && (m[i - 1][j] == 0)) {
                m[i - 1][j] = fill;
                fill--;
                moveUp(i - 1, j);
            } else moveLeft(i, j);
        }
    }

    const moveLeft = (i, j) => {
        if (fill > 0) {

            if ((j - 1 >= 0) && (m[i][j - 1] == 0)) {
                m[i][j - 1] = fill;
                fill--;
                moveLeft(i, j - 1);
            } else moveDown(i, j);
        }

    }

    const moveRight = (i, j) => {
        if (fill > 0) {

            if ((j + 1 <= n - 1) && (m[i][j + 1] == 0)) {
                m[i][j + 1] = fill;
                fill--;
                moveRight(i, j + 1);
            } else moveUp(i, j);
        }
    }

    m[0][0] = n * n

    moveDown(0, 0);

    return m;

}

//Problem 5.1
const lib = require("./library.js");

let matrix1 = [
    [1, 2, 3],
    [1, 2, 4],
    [1, 2, 5]
];


const fiveA = () => {
    lib.saveMatrixToFile(matrix1, "./matrices.txt");

}


const fiveB = () => {
    let matrix2 = lib.loadMatrixFromFile("./matrices.txt");
    console.log(matrix2);
}

fiveA();
fiveB();

//Problem 5.2

const fs = require("fs");

const matToStr = (m) => {
    let result = "";
    for (let i = 0; i < m.length; i++) {
        for (let j = 0; j < m[i].length; j++) {
            result += m[i][j] + "\t";

        }
        result += "\n";
    }
    return result;
}


const saveMatrixToFile = (matrix, path) => {
    let stringedMatrix = matToStr(matrix);
    fs.writeFile(path, stringedMatrix, () => { });
}

const loadMatrixFromFile = (path) => {
    let stringedMat = fs.readFileSync(path, "utf-8");

    return stringedMat;
}

module.exports = { loadMatrixFromFile, saveMatrixToFile };
