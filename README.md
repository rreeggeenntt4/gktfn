# gktfn
------------------------------------------------------
Реализовать функцию:

        function normalize($input)
        {
            /* return "<not implemented yet>"; */
        }

        $input1 = "/var/./lib/../test";
        $input2 = "/var/lib/../../test";
        $input3 = "/var/lib1/lib2/lib3/././././././lib4/../../../../lib5";

        $output1 = normalize($input1);
        $output2 = normalize($input2);
        $output3 = normalize($input3);


        echo $output1 . "\n"; // expected output: /var/test
        echo $output2 . "\n"; // expected output: /test
        echo $output3 . "\n"; // expected output: /var/lib5 


------------------------------------------------------
Решение:

        function normalize($input)
        {
            $patterns = array('~/{2,}~', '~/(\./)+~', '~([^/\.]+/(?R)*\.{2,}/)~', '~\.\./~');
            $replacements = array('/', '/', '', '');
            return preg_replace($patterns, $replacements, $input);
        }

        $input1 = "/var/./lib/../test";
        $input2 = "/var/lib/../../test";
        $input3 = "/var/lib1/lib2/lib3/././././././lib4/../../../../lib5";

        $output1 = normalize($input1);
        $output2 = normalize($input2);
        $output3 = normalize($input3);


        echo $output1 . "\n"; // expected output: /var/test
        echo $output2 . "\n"; // expected output: /test
        echo $output3 . "\n"; // expected output: /var/lib5 