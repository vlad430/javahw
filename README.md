# javahw

* Vlad Varchuk

package org.itstep;

import java.util.*;
import java.util.stream.Collectors;

public class StreamsHomework {

	private enum Sex {
        MAN,
        WOMEN
    }

    private static class Student {
        private final String name;
        private final Integer age;
        private final Sex sex;

        public Student(String name, Integer age, Sex sex) {
            this.name = name;
            this.age = age;
            this.sex = sex;
        }

        public String getName() {
            return name;
        }

        public Integer getAge() {
            return age;
        }

        public Sex getSex() {
            return sex;
        }

        @Override
        public String toString() {
            return "{" +
                    "name='" + name + '\'' +
                    ", age=" + age +
                    ", sex=" + sex +
                    '}';
        }
        
        @Override
        public boolean equals(Object o) {
            if (this == o) return true;
            if (!(o instanceof Student)) return false;
            Student people = (Student) o;
            return Objects.equals(name, people.name) &&
                    Objects.equals(age, people.age) &&
                    Objects.equals(sex, people.sex);
        }

        @Override
        public int hashCode() {
            return Objects.hash(name, age, sex);
        }
    }
	
    static Collection<Student> students = Arrays.asList(
            new Student("Вася", 16, Sex.MAN),
            new Student("Петя", 23, Sex.MAN),
            new Student("Соня", 18, Sex.WOMEN),
            new Student("Виктор Петрович", 65, Sex.MAN),
            new Student("Дима", 25, Sex.MAN),
            new Student("Катя", 21, Sex.WOMEN),
            new Student("Семен", 33, Sex.MAN),
            new Student("Елена", 42, Sex.WOMEN),
            new Student("Иван Иванович", 69, Sex.MAN)
    );
    
    static List<Student> ex01() {
    	// TODO: Задание 1
    	// Выбрать всех мужчин-военнообязанных (возраст от 18 до 27 лет)
        List<Student> students1 = students.stream()
                         .filter(s -> s.getSex().equals(Sex.MAN))
                         .filter(s -> s.getAge()>18&&s.getAge()<27)
                         .collect(Collectors.toList());
    	return students1;
    }
    
    static Double ex02() {
    	// TODO: Задание 2
    	// Найти средний возраст среди мужчин
        double avg = students.stream()
                .filter(s -> s.getSex().equals(Sex.MAN))
                .mapToDouble(s ->s.getAge())
                .average().getAsDouble();
    	return avg;
    }
    
    static Long ex03() {
    	// TODO: Задание 3
    	// Найти кол-во потенциально работоспособных 
    	// студентов в выборке (т.е. от 18 лет и учитывая 
    	// что женщины выходят в 55 лет, а мужчина в 60)
        Long l = students.stream()
                .filter(s -> s.getAge()>18)
                .filter(s -> s.getAge()<60)
                .filter(s -> s.getSex().equals(Sex.MAN)&&s.getAge()<60||s.getSex().equals(Sex.WOMEN)&&s.getAge()<55)
                .count();
    	return l;
    	
    }
    
    static List<Student> ex04() {
    	// TODO: Задание 4    	
    	// Отсортировать студентов по имени в обратном алфавитном порядке
        List <Student> s1 = students.stream()
                .sorted(Comparator.comparing(Student::getName).reversed())
                .collect(Collectors.toList());
    	return s1;
    }
    
    static Student ex05() {
    	//  TODO: Задание 5
    	//  найти самого старшего студента
        Student i = students.stream()
                .max(Comparator.comparingInt(Student::getAge))
                .get();
    	return i;
    }
    
    static Student ex06() {
    	// TODO: Задание 6
    	// Найти самого младшего студента
        Student i = students.stream()
                .min(Comparator.comparingInt(Student::getAge))
                .get();
    	return i;
    }
    
    public static void main(String[] args) {
		// TODO: тестировать здесь
        System.out.println(ex01());
        System.out.println(ex02());
        System.out.println(ex03());
        System.out.println(ex04());
        System.out.println(ex05());
        System.out.println(ex06());
	}
} 
