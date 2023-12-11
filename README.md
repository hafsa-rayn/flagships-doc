# FLAGDPS - Style Guide

This style guide is mostly based on the standards that are currently prevalent in JavaScript.

## Table of Contents

  1. [Basic Rules](#basic-rules)
  1. [Naming](#naming)
  1. [Declaration](#declaration)
  1. [Alignment](#alignment)
  2. [Types](#types)
  1. [Quotes](#quotes)
  1. [Spacing](#spacing)
  1. [Props](#props)
  1. [Parentheses](#parentheses)
  1. [Tags](#tags)

## Basic Rules

  - **Folder Structure**:
    - Organize each feature within its dedicated folder in the feature directory.
    - Within each feature folder, include separate directories for components, types, and queries.
    - Centralize reusable or shared elements in the shared folder.
    - Only include one React component per file.
      - However, multiple [Stateless, or Pure, Components](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions) are allowed per file. eslint: [`react/no-multi-comp`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless)
        
  - **Styling**:
    - Prioritize the use of Ant Design components over custom-coded components
    - Favor Ant Design styling, for example using Ant Design flex for layout
    - For Ant Design global component styling, incorporate it in `shared/providers/theme.ts`
    - If custom styles are necessary, create a .less file specific to that component
   
  - **Comments**:
    - Include a concise comment for each component to explain its purpose.

## Naming

  - **Extensions**: Use `.jsx` extension for React components. eslint: [`react/jsx-filename-extension`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-filename-extension.md)
  - **Filename**: Use CamelCase for filenames. E.g., `reservationCard.jsx`.
  - **Foldername**: Use smallcase for foldernames. E.g., `farmdata`. Use CamelCase if absolutely necessary.
  - **Reference Naming**: Use CamelCase for React components and camelCase for their instances. eslint: [`react/jsx-pascal-case`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

    ```jsx
    // bad
    import reservationCard from './ReservationCard';

    // good
    import ReservationCard from './ReservationCard';

    // bad
    const ReservationItem = <ReservationCard />;

    // good
    const reservationItem = <ReservationCard />;
    ```


## Alignment

  - Follow these alignment styles for JSX syntax. eslint: [`react/jsx-closing-bracket-location`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md) [`react/jsx-closing-tag-location`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-closing-tag-location.md)

    ```jsx
    // bad
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // good
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // if props fit in one line then keep it on the same line
    <Foo bar="bar" />

    // children get indented normally
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Quux />
    </Foo>

    // bad
    {showButton &&
      <Button />
    }

    // bad
    {
      showButton &&
        <Button />
    }

    // good
    {showButton && (
      <Button />
    )}

    // good
    {showButton && <Button />}

    // good
    {someReallyLongConditional
      && anotherLongConditional
      && (
        <Foo
          superLongParam="bar"
          anotherSuperLongParam="baz"
        />
      )
    }

    // good
    {someConditional ? (
      <Foo />
    ) : (
      <Foo
        superLongParam="bar"
        anotherSuperLongParam="baz"
      />
    )}
    ```

## Types
  - Define types consistently throughout the codebase and organize them in their respective types folder.
  
## Quotes

  - Always use single quotes (`'`) for all. prettier: [`singleQuote: true,`](https://eslint.org/docs/rules/jsx-quotes)

    > Why? Just so

    ```jsx
    // bad
    <Foo bar="bar" />

    // good
    <Foo bar='bar' />

    // bad
    <Foo style={{ left: "20px" }} />

    // good
    <Foo style={{ left: '20px' }} />
    ```

## Spacing

  - Always include a single space in your self-closing tag. eslint: [`no-multi-spaces`](https://eslint.org/docs/rules/no-multi-spaces), [`react/jsx-tag-spacing`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-tag-spacing.md)

    ```jsx
    // bad
    <Foo/>

    // very bad
    <Foo                 />

    // bad
    <Foo
     />

    // good
    <Foo />
    ```

  - Do not pad JSX curly braces with spaces. eslint: [`react/jsx-curly-spacing`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-curly-spacing.md)

    ```jsx
    // bad
    <Foo bar={ baz } />

    // good
    <Foo bar={baz} />
    ```

## Props

  - Always use camelCase for prop names, or PascalCase if the prop value is a React component.

    ```jsx
    // bad
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    // good
    <Foo
      userName="hello"
      phoneNumber={12345678}
      Component={SomeComponent}
    />
    ```

  - Omit the value of the prop when it is explicitly `true`. eslint: [`react/jsx-boolean-value`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-boolean-value.md)

    ```jsx
    // bad
    <Foo
      hidden={true}
    />

    // good
    <Foo
      hidden
    />

    // good
    <Foo hidden />
    ```

  - Always include an `alt` prop on `<img>` tags. If the image is presentational, `alt` can be an empty string or the `<img>` must have `role="presentation"`. eslint: [`jsx-a11y/alt-text`](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y/blob/master/docs/rules/alt-text.md)

    ```jsx
    // bad
    <img src="hello.jpg" />

    // good
    <img src="hello.jpg" alt="Me waving hello" />

    // good
    <img src="hello.jpg" alt="" />

    // good
    <img src="hello.jpg" role="presentation" />
    ```

  - Do not use `accessKey` on elements. eslint: [`jsx-a11y/no-access-key`](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y/blob/master/docs/rules/no-access-key.md)

    > Why? Inconsistencies between keyboard shortcuts and keyboard commands used by people using screenreaders and keyboards complicate         accessibility.

    ```jsx
    // bad
    <div accessKey="h" />
  
    // good
    <div />
    ```

  - Avoid using an array index as `key` prop, prefer a stable ID. eslint: [`react/no-array-index-key`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/no-array-index-key.md)

    > Why? Not using a stable ID [is an anti-pattern](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)            because it can negatively impact performance and cause issues with component state.

    We don’t recommend using indexes for keys if the order of items may change.

      ```jsx
      // bad
      {todos.map((todo, index) =>
        <Todo
          {...todo}
          key={index}
        />
      )}
    
      // good
      {todos.map(todo => (
        <Todo
          {...todo}
          key={todo.id}
        />
      ))}
      ```

  - Always define explicit default for all non-required .

    > Why? propTypes are a form of documentation, and providing default means the reader of your code doesn’t have to assume as much. In          addition, it can mean that your code can omit certain type checks.

      ```jsx
    
      type NumbersOverviewCard = {
        heading: string | ReactElement
        digit: number
        isLoading: boolean
        tooltipData?: string | undefined
      }
    
      // good
        export const NumbersOverviewCard = ({
        heading,
        digit,
        isLoading,
        tooltipData = undefined,
      }
    
      // bad
       export const NumbersOverviewCard = ({
        heading,
        digit,
        isLoading,
        tooltipData = undefined,,
      }
      ```

  - Use spread  sparingly.
  > Why? Otherwise you’re more likely to pass unnecessary  down to components. And for React v15.6.1 and older, you could [pass invalid HTML attributes to the DOM](https://reactjs.org/blog/2017/09/08/dom-attributes-in-react-16.html).

  Exceptions:

  - HOCs that proxy down  and hoist propTypes

    ```jsx
    function HOC(WrappedComponent) {
      return class Proxy extends React.Component {
        Proxy.propTypes = {
          text: PropTypes.string,
          isLoading: PropTypes.bool
        };
  
        render() {
          return <WrappedComponent {...this.} />
        }
      }
    }
    ```

  Notes for use:
  Filter out unnecessary props when possible. Also, use [prop-types-exact](https://www.npmjs.com/package/prop-types-exact) to help prevent bugs.

## Parentheses

  - Wrap JSX tags in parentheses when they span more than one line. eslint: [`react/jsx-wrap-multilines`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-wrap-multilines.md)

    ```jsx
    // bad
    render() {
      return <MyComponent variant='long body' foo='bar'>
               <MyChild />
             </MyComponent>;
    }

    // good
    render() {
      return (
        <MyComponent variant='long body' foo='bar'>
          <MyChild />
        </MyComponent>
      );
    }

    // good, when single line
    render() {
      const body = <div>hello</div>;
      return <MyComponent>{body}</MyComponent>;
    }
    ```

## Tags

  - Always self-close tags that have no children. eslint: [`react/self-closing-comp`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)

    ```jsx
    // bad
    <Foo variant="stuff"></Foo>

    // good
    <Foo variant="stuff" />
    ```

  - If your component has multiline properties, close its tag on a new line. eslint: [`react/jsx-closing-bracket-location`](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

    ```jsx
    // bad
    <Foo
      bar='bar'
      baz='baz' />

    // good
    <Foo
      bar='bar'
      baz='baz'
    />
    ```


**[⬆ back to top](#table-of-contents)**
