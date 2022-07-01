package coverage

import (
	"errors"
	"os"
	"reflect"
	"strconv"
	"testing"
	"time"
)

func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

var p = People{Person{
	firstName: "John",
	lastName:  "Doe",
	birthDay:  time.Date(1970, 1, 1, 0, 0, 1, 0, time.UTC),
}, Person{
	firstName: "Napoleon",
	lastName:  "Bonapart",
	birthDay:  time.Date(1775, 12, 5, 7, 49, 54, 0, time.UTC),
}, Person{
	firstName: "John",
	lastName:  "Smith",
	birthDay:  time.Date(1970, 1, 1, 0, 0, 1, 0, time.UTC),
}, Person{
	firstName: "James",
	lastName:  "Vega",
	birthDay:  time.Date(1970, 1, 1, 0, 0, 1, 0, time.UTC),
}}

func TestPeopleLen(t *testing.T) {
	if len(p) != p.Len() {
		t.Errorf("Len() method is not correct: Must be %d but have %d.\n", len(p), p.Len())
	}

}

func TestPeopleLess(t *testing.T) {
	if less := p.Less(0, 1); !less {
		t.Errorf("People[%d] must be < than People[%d]", 0, 1)
	}
	if less := p.Less(3, 0); !less {
		t.Errorf("People[%d] must be < than People[%d]", 3, 0)
	}
	if less := p.Less(0, 2); !less {
		t.Errorf("People[%d] must be < than People[%d]", 0, 2)
	}
}

func TestPeoplePeopleSwap(t *testing.T) {
	now := time.Now()

	A := Person{
		firstName: "A",
		lastName:  "A",
		birthDay:  now.Add(time.Minute)}
	B := Person{
		firstName: "B",
		lastName:  "B",
		birthDay:  now.Add(time.Minute)}

	p1 := People{A, B}
	p2 := People{B, A}
	if p1.Swap(0, 1); !reflect.DeepEqual(p1, p2) {
		t.Fail()
	}
}

func TestMatrixNew(t *testing.T) {
	ref := &Matrix{
		rows: 3,
		cols: 3,
		data: []int{1, 2, 3, 4, 5, 6, 7, 8, 9},
	}
	if mm, err := New("1 2 3\n4 5 6\n7 8 9"); err != nil {
		t.Error(err.Error())
	} else if !reflect.DeepEqual(ref, mm) {
		t.Errorf("got: %v got: %v\n", mm, ref)
	}

	wrong := "1 2 3\n4 5 6\n"
	if _, err := New(wrong); err == nil {
		t.Error("Rows not eq Cols")
	}

	atoiErr := "1 2 3\n4 a 6\n7 8 9"
	if _, err := New(atoiErr); err != nil {
		if !errors.Is(err, strconv.ErrSyntax) {
			t.Error(err.Error())
		}
	}
}

func TestMatrixCols(t *testing.T) {
	matrix, err := New("1 2 3\n4 5 6\n7 8 9")
	if err != nil {
		t.Errorf("Error on New matrix: %s\n", err.Error())
	}
	refCols := [][]int{{1, 4, 7}, {2, 5, 8}, {3, 6, 9}}
	if cols := matrix.Cols(); !reflect.DeepEqual(cols, refCols) {
		t.Errorf("Error on matrix.Cols(): not equal\nGot: %v, want: %v\n", cols, refCols)
	}
}

func TestMatrixRows(t *testing.T) {
	matrix, err := New("1 2 3\n4 5 6\n7 8 9")
	if err != nil {
		t.Errorf("Error on New matrix: %s\n", err.Error())
	}

	refRows := [][]int{{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}
	if rows := matrix.Rows(); !reflect.DeepEqual(rows, refRows) {
		t.Errorf("Error on matrix.Rows(): not equal\nGot: %v, want: %v\n", rows, refRows)
	}
}
func TestMatrixSet(t *testing.T) {
	defMatrix := &Matrix{rows: 3, cols: 3, data: []int{1, 2, 3, 4, 5, 6, 7, 8, 9}}
	refMatrix := &Matrix{rows: 3, cols: 3, data: []int{1, 2, 3, 4, 5, 6, 7, 8, -1}}

	// change [3][3] element
	if ok := defMatrix.Set(2, 2, -1); !ok {
		if !reflect.DeepEqual(refMatrix, defMatrix) {
			t.Errorf("Target not changed. Bug in method?\n")
		}
	}

	// change out of range element. should be false.
	if ok := defMatrix.Set(5, 5, -1); ok {
		t.Errorf("Unpresent target changed. Bug in method?\n")
	}

}
