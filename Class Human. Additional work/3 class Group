import java.io.*;
import java.util.Arrays;

public class Group implements Voenkom {

    private String groupName = "?";
    private Student[] groupList = new Student[10];

    public Group() {
    }

    public Group(String groupName) {
        this.groupName = groupName;
    }

    public String getGroupName() {
        return groupName;
    }

    public void setGroupName(String groupName) {
        this.groupName = groupName;
    }

    public void addStudent(Student newStudent){
        if(newStudent.getGroup() == null) { //проверяем не учится ли этот студент уже в какойто группе
            boolean isAdd = false; //успешно ли добавлен студент?
            for (int i = 0; i < groupList.length; i++) {
                if (groupList[i] == null) { //если место в группе свободно
                    groupList[i] = newStudent; //добавляем на свободное место
                    newStudent.setGroup(this); //указываем что студент теперь учится в этой группе
                    System.out.println("Student " + newStudent.getSurname() + " is added to the group: " + groupName);
                    isAdd = true;
                    break;
                }
            }
            try {
                if (!isAdd){
                    throw new FullGroupException(); //если студет не добавлен, так как нет места
                }
            } catch (FullGroupException e) {
                System.out.println("The group is full ");
            }
            //если этот студент уже есть в какойто группе
        } else System.out.println("Student " + newStudent.getSurname() + " already studying in group: " + newStudent.getGroup().getGroupName());
    }

    private class FullGroupException extends Exception{}

    public void addStudent(){ // для интерактивного добавления студента, тоже метод, но без параметра (студента создадим в процессе)
        int freePlace = -1; // cюда запишем номер свободного места
        for (int i = 0; i < groupList.length; i++) { //иещем есть ли свободное место
            if (groupList[i] == null) { //если место в группе свободно
                freePlace = i;
                System.out.println("Free place was found in group " + groupName + ". Please enter student data ");
                break;
            }
        }
        if(freePlace < 0){ //если места не нашлось
            System.out.println("The group is full");
        }
        else { //если нашли место
            while (true) { //для повтора попытки добавления студента если был некорректный ввод данных
                Student st = new Student();
                BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
                try {
                    System.out.println("Please enter student surname (String):");
                    st.setSurname(reader.readLine());
                    System.out.println("Please enter student name (String):");
                    st.setName(reader.readLine());
                    System.out.println("Please enter student sex (man / woman):");
                    st.setSex(reader.readLine().equals("man"));
                    System.out.println("Please enter student age (int 1-100):");
                    st.setAge(Integer.parseInt(reader.readLine()));
                    System.out.println("Please enter student height (int 1-300):");
                    st.setHeight(Integer.parseInt(reader.readLine()));
                    System.out.println("Please enter student weight (int 1-300):");
                    st.setWeight(Integer.parseInt(reader.readLine()));
                    System.out.println("Please enter student course (int 1-6):");
                    st.setCourse(Integer.parseInt(reader.readLine()));
                    System.out.println("Please enter student studBook (int 1-10000):");
                    st.setStudBook(Integer.parseInt(reader.readLine()));
                    System.out.println("Please enter student averageRating (int 1.0-5.0):");
                    st.setAverageRating(Double.parseDouble(reader.readLine()));
                    groupList[freePlace] = st; //добавляем на свободное место
                    st.setGroup(this); //указываем что студент теперь учится в этой группе
                    System.out.println("Student " + st.getSurname() + " is added to the group: " + groupName);
                    break;
                }
                catch (Exception e) { //если ввели некоректные данные предлагаем попробовать еще раз
                    System.out.println("Invalid enter, student is not added, try again? (y / n):");
                    try {
                        if (reader.readLine().equals("y")) {
                            System.out.println("Please enter student data:");
                        }
                        else { //при любом вводе отличном от "y" заканчиваем попытки добавить студента
                            break;
                        }
                    }
                    catch (Exception x){ //любой ввод будет коректным, но reader.readLine() считается опаснм потому обработаем
                        System.out.println("Invalid enter");
                        break;
                    }
                }
            }
        }
    }

    public void delStudent(String surname){ //удаление по фамилии
        int countSt = 0;
        for(Student st : groupList){  //пересчитаем сколько студентов с такой фамилией в группе
            if (st!=null && st.getSurname().equals(surname)){
                countSt++;
            }
        }
        if(countSt == 0){
            System.out.println("No student " + surname + " in "  + groupName + " group"); //если студентов нет
        }
        if(countSt == 1){ //если один студент, то удаляем
            for(int i = 0; i < groupList.length; i++){
                if(groupList[i]!=null && groupList[i].getSurname().equals(surname)) {
                    groupList[i].setGroup(null); //указываем что студент теперь не учится ни в какой группе
                    groupList[i] = null; //удаляем студента
                    sortGroupListAfterDelStudent(); // убираем дырку null в массиве после удаления
                    System.out.println("Student " + surname + " is deleted from the group" + groupName);
                    break;
                }
            }
        }
        if(countSt > 1){ //если больше одного
            System.out.println("Student " + surname + " in group " + groupName + " more then 1!"); //сообщаем что студентов больше 1
            searchStudent(surname); // показываем нумерованный список студентов с такой фамилией
            System.out.println("Please use the method delStudent(int number)"); //просим удалить по номеру
        }
    }

    public void delStudent(int number){ //удаляем студента по номеру в группе
        try {
            String bufferStudSurname = groupList[number-1].getSurname(); //запоминаем фамилию студента чтоб вывести сообщение после удаления
            groupList[number-1].setGroup(null); //указываем что студент теперь не учится ни в какой группе
            groupList[number-1] = null; //удаляем студента
            sortGroupListAfterDelStudent(); // убираем дырку null в массиве после удаления
            System.out.println("Student " + bufferStudSurname + " is deleted from the group" + groupName);
        }
        catch(ArrayIndexOutOfBoundsException e){
            System.out.println("Invalid student number");
        }
    }

    private void sortGroupListAfterDelStudent(){ // убираем дырку null в массиве после удаления
        for(int i = 0; i < groupList.length-1; i++){//проходим по всем элементам кроме последнего
            if(groupList[i] == null && groupList[i+1] != null){
                groupList[i] = groupList[i+1];
                groupList[i+1] = null;
            }
        }
    }

    public void searchStudent(String surname){ //поиск всех студентов с такой фамилией
        boolean isFound = false; //найден ли хотябы один студент с требуемой фамилией
        for(int i = 0; i < groupList.length; i++){
                if (groupList[i]!=null && groupList[i].getSurname().equals(surname)) {
                    System.out.println("Student " + surname + " is found in group. List number is " + (i + 1) + ".");
                    groupList[i].info();
                    isFound = true;
                }
        }
        if(!isFound){
            System.out.println("No student " + surname + " in "  + groupName + " group"); //если не найден
        }
    }


    @Override
    public String toString() {
        return stListToString(groupList);
    }

     String stListToString (Student[] arr){ //выносим конвертацию массива в строку, та как она нужна в нескольких методах
        StringBuilder sb = new StringBuilder();
        sb.append("groupName=");
        sb.append(groupName);
        sb.append("\n");
        for(Student st : arr){
            if(st==null) {
                break;
            }
            sb.append(st);
            sb.append("\n");
        }
        return sb.toString();
    }

    public void sortSurnameAndPrint(){ //сортировка студентов в алфавитном порядке + печать списка
        Student[] sortList = arrWithoutNull(groupList);
        Arrays.sort(sortList);
        /*
        for(int i = 0; i < sortList.length-1; i++){
            for(int y = i+1; y < sortList.length; y++){
                if(sortList[i]!=null && sortList[y]!=null && sortList[i].getSurname().compareTo(sortList[y].getSurname()) > 0 ){
                    Student buffer = sortList[i];
                    sortList[i] = sortList[y];
                    sortList[y] = buffer;
                }
            }
        }
        */
        System.out.println("afterSurnameSort");
        System.out.println(stListToString(sortList));
    }

    private Student[] arrWithoutNull(Student[] arr){ //вспомогательный метод который вернет массив без null в конце, если они есть
        int stCounter = 0;
        for(Student st : arr){
            if(st==null){
                break;
            }
            stCounter++;
        }
        Student[] sortList = new Student[stCounter];
        System.arraycopy (arr, 0, sortList, 0, stCounter);
        return sortList;
    }

    public void sortAndPrint(){ //интерактивная сортировка + печать
        Student[] sortList = new Student[groupList.length];
        System.arraycopy (groupList, 0, sortList, 0, groupList.length);

        System.out.println("Please enter parameter of sort(surname/name/age/height/weight/studBook/averageRating):");
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        try {
            String s = reader.readLine();
            boolean invalidEnter = true; //сюда запишем верный ли ввод параметра
            if(s.equals("surname")){
                Arrays.sort(sortList, (sOne, sTwo) -> (sOne == null || sTwo == null) ? 1 : sOne.getSurname().compareTo(sTwo.getSurname()));
                System.out.println("after Surname Sort");
                System.out.println(stListToString(sortList));
                invalidEnter = false;
            }
            if(s.equals("name")){
                Arrays.sort(sortList, (sOne, sTwo) -> (sOne == null || sTwo == null) ? 1 : sOne.getName().compareTo(sTwo.getName()));
                System.out.println("after Name Sort");
                System.out.println(stListToString(sortList));
                invalidEnter = false;
            }
            if(s.equals("age")){
                Arrays.sort(sortList, (sOne, sTwo) -> (sOne == null || sTwo == null) ? 1 : sOne.getAge() - sTwo.getAge());
                System.out.println("after Age Sort");
                System.out.println(stListToString(sortList));
                invalidEnter = false;
            }
            if(s.equals("height")){
                Arrays.sort(sortList, (sOne, sTwo) -> (sOne == null || sTwo == null) ? 1 : sOne.getHeight() - sTwo.getHeight());
                System.out.println("after Height Sort");
                System.out.println(stListToString(sortList));
                invalidEnter = false;
            }
            if(s.equals("weight")){
                Arrays.sort(sortList, (dOne, dTwo) -> (dOne == null || dTwo == null) ? 1 : dOne.getWeight() - dTwo.getWeight());
                System.out.println("after Weight Sort");
                System.out.println(stListToString(sortList));
                invalidEnter = false;
            }
            if(s.equals("studBook")){
                Arrays.sort(sortList, (dOne, dTwo) -> (dOne == null || dTwo == null) ? 1 : dOne.getStudBook() - dTwo.getStudBook());
                System.out.println("after StudBook Sort");
                System.out.println(stListToString(sortList));
                invalidEnter = false;
            }
            if(s.equals("averageRating")){
                Arrays.sort(sortList, (sOne, sTwo) -> (sOne == null || sTwo == null) ? 1 : (sOne.getAverageRating() - sTwo.getAverageRating() > 0)? -1:1);
                System.out.println("after AverageRating Sort");
                System.out.println(stListToString(sortList));
                invalidEnter = false;
            }
            if(invalidEnter){
                throw new Exception();
            }
        }
        catch (Exception e){
            System.out.println("Invalid enter");
        }
    }

    @Override
    public Student[] getStudentValidForArmy() { //метод вернет масив юношей старше 18 лет
        Student[] studentValidForArmy = new Student[groupList.length];
        int counterOfValidStudent = 0;
        for(int i = 0; i < groupList.length; i++) {
            if (groupList[i] != null && groupList[i].isSex() && groupList[i].getAge() >= 18) {
                studentValidForArmy[counterOfValidStudent] = groupList[i];
                counterOfValidStudent++;
            }
        }
        return arrWithoutNull(studentValidForArmy);
    }

    public void printGroupToFile(String resultFolderAdress) throws IOException {
        if(resultFolderAdress == null){
            throw new IllegalArgumentException("nulPointer");
        }
        File folderResult = new File(resultFolderAdress);
        if (!folderResult.exists()) {
            folderResult.mkdir();
        }

        File fileResult = new File(resultFolderAdress + "/result.stgroup");

        try{
            fileResult.createNewFile();
        }
        catch(IOException e){
            System.out.println(e);
        }

        try(BufferedWriter f = new BufferedWriter(new FileWriter(fileResult))){ 
            f.write(groupName + "\n");
            for(Student st: groupList) {
                if(st!=null) {
                    f.write(st.printStudentToFile() + "\n");
                }
            }
        }
        catch(IOException e){
            System.out.println(e);
        }
    }

    public static Group redGroupFromFile(String fileAdress) throws IOException {
        if (fileAdress == null) {
            throw new IllegalArgumentException("nulPointer");
        }
        int pointerIndex = fileAdress.lastIndexOf(".");
        String ext = fileAdress.substring(pointerIndex + 1);

        File groupFile = new File(fileAdress);
        if (!groupFile.exists() || !groupFile.isFile() || !ext.equals("stgroup")) {
            throw new IllegalArgumentException("file not exists or is not file or not stgroup");
        }

        Group groupFromFile = new Group();
        boolean groupNameInitialise = false;

        try(BufferedReader f = new BufferedReader(new FileReader(groupFile))){
            for(String str="";( str = f.readLine())!=null ; ) {
                if(!groupNameInitialise){
                    groupFromFile.setGroupName(str);
                    groupNameInitialise = true;
                    continue; 
                }
                String[] s = str.split(";");
                String surname = s[0];
                String name = s[1];
                boolean sex = Boolean.parseBoolean(s[2]);
                int age = Integer.parseInt(s[3]);
                int height = Integer.parseInt(s[4]);
                int weight = Integer.parseInt(s[5]);
                int course = Integer.parseInt(s[6]);
                int studBook = Integer.parseInt(s[7]);
                double averageRating = Double.parseDouble(s[8]);

                groupFromFile.addStudent(new Student(surname,name,sex,course,studBook,averageRating,age,height,weight));
            }
        }
        catch(IOException e){
            System.out.println("ERROR");
        }
        return groupFromFile;
    }
}