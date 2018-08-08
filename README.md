# React Patterns

## Presentational

## Layout Component
```jsx
class Card extends React.Component {
  render() {
    return (
      <div className="card">
        <div className="card--content">
          <div className="card--left-panel">
            {this.props.leftPanel()}
          </div>
          <div className="card--right-panel">
            {this.props.rightPanel()}
          </div>
        </div>
        <footer className="card--footer">
          {this.props.footer()}
        </footer>
      </div>
    )
  }
}

// Usage
<Card
  rightPanel={() => {
    <Badge />
  })}
  leftPanel={() => {
    return (
      <div>
        ...
      </div>
    )
  }}

  footer={() => {
    return (
      <div>
        ...
      </div>
    )
  }}
/>

// Alternative
<Card>
  <LeftPanel />
  <RightPanel />
  <Footer />
</Card>
```

### With Controls
```jsx
class Parent extends React.Component {
  toggleModal = () => {
    this.state.modalOpen = !this.state.modalOpen;
  }

  render() {
    <div className="parent">
      <div className="parent--body">
        ....
        <button onClick={this.toggleModal}>Login</button>
      </div>`
      <Modal isOpen={this.state.modalOpen} handleModal={this.toggleModal}/>
    </div>
  }
}

class Modal extends React.Component {
  render() {
    this.props.isOpen
      &&
    (
      <div className="modal">
        <button onClick={this.props.handleModal}>x</button>
        <div className="modal--body">
          {this.props.body()}
        </div>
        <div className="modal--footer">
          {this.props.footer()}
        </div>
      </div>
    )
  }
}
```

## Render Props (Behavior)
- abstraction of behavior
- possible pass props down deep into component tree

Alternatives
- 16.3 Context API
- HOC

### Data Request
```jsx
class Request extends React.Component {
  state = {
    loading: true,
    error: null,
    data: {}
  }

  componentDidMount() {
    this.getData();
  }

  getData = async() => {
    try {
      const data = await axios.get(this.props.url);
      this.setState({ data, loading: false});
    } catch(error) {
      this.setState({ error, loading: false})
    }
  }

  render() {
    const { loading, error, data} = this.state;

    return (
      {this.props.render(loading, error, data)}
    );
  }
}

const ApplicantList = () => {
  return (
    <Request
      url={'api.chingu.io/applicants'}
      render=(({error, loading, data}) => {
        if (error) return <Error error={error} />;
        if (loading) return <Loader ...  />;

        return (
          <div>
            <h2>Applicant List</h2>
            <ul>
              {data.map(applicant => {
                <li>applicant</li>
              })}
            </ul>
          </div>
        );
      })
    />
  )
}
```

### Queries/Mutations
See:
- https://www.apollographql.com/docs/react/essentials/queries.html
- https://www.apollographql.com/docs/react/essentials/mutations.html


### MultiPartForm
```jsx
class MultiPartForm extends React.Component {

  this.state = {
    currentPage: 0,
    totalPages: this.props.children.count() - 1
  }

  next() {
    this.setState((prevState) => {
      return {
        {
          currentPage: prevState.currentPage + 1;
        }
      }
    });
  }

  prev() {
    this.setState((prevState) => {
      return {
        currentPage: prevState.currentPage === 0 ? 0 : prevState.currentPage - 1;
      }
    })
  }

  render() {
    if (this.props.multipage) {
    return (
      <div>
        {this.props.children.map((child, index) => {
          if (index == this.state.currentPage) {
            return React.cloneElement(child, {
              ...props
            });
          }
        })}
        <div>
          <button onClick={this.next}>next</button>
          <button onClick={this.back}>prev</button>
        </div>
      <div>
    )
    } else {
      {/* ... single page stitch ... */
    }

  }
}

// usage
 <MultiPartForm multipage>
  <PartialForm />
  <PartialForm />
  <PartialForm />
  <PartialForm />
  <PartialForm />
 </MultiPartForm>

<MultiPartForm>
  <PartialForm />
 </MultiPartForm>
```

### Switch Component
```jsx
class Switch extends React.Component {

}

const SwitchExample = () => {
  return (
    <Switch>
      <Form />
      <Form />
      <Form />
      <Form />
      <Complete />
    </Switch>
  )
}
```

### Local Storage
```jsx
class LocalStorage extends React.Component {
}
```

## Provider

### Render Props

### Context API

### HOC

## Component Sync (Issues)
- Header.js

## DOM manipulation outside of React

## Breaking up components
- Should be done when doing more than what you can hold in your working memory

## Directory Structure
